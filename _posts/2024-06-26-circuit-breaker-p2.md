---
layout: post
permalink: "/post/software-engineering/circuit-breaker-p2"
title:  "Software Resilience w/ Circuit Breaker p.2"
date:   2024-08-22 23:05:00 +1100
---

Hey there! It's been a while..
<br/>
<br/>
Got caught up with some stuff which is a bad excuse but hey, here I am trying to get back at it again.
<br/>
If you were anticipating the demo, here you go..
<br/>

![CircuitBreaker](/assets/CircuitBreaker.gif)

Now that you've caught a glimpse, let's break it into these sections:
1. Creating a simple demo api producer
    - this will act as a third party api in your real world solution where it's kindof flaky/faulty/unstable.
2. Breakdown the circuit breaker implementation

Let's get started!


### Creating a simple demo api producer

First thing's first..
Let's create a blank web api project.
(If you already know how to create one in either vs/vscode, you can keep scrolling.)

For my case, I prefer using Visual Studio rather than VS Code.

#### Step 1: Create a new project

![CircuitBreakerDemo](/assets/circuit-breaker-p2-sol-1.png)

![CircuitBreakerDemo](/assets/circuit-breaker-p2-sol-2.png)

![CircuitBreakerDemo](/assets/circuit-breaker-p2-sol-3.png)

![CircuitBreakerDemo](/assets/circuit-breaker-p2-sol-4.png)

#### Step 2: Create a new controller

![CircuitBreakerDemo](/assets/circuit-breaker-p2-sol-5.png)

Add the code below:

```cs
using Microsoft.AspNetCore.Mvc;

namespace CircuitBreakerDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class ProducerController : ControllerBase
    {
        private static int requestCount = 0;
        private static readonly object lockObj = new object();

        [HttpGet]
        public IActionResult Get()
        {
            lock (lockObj)
            {
                requestCount++;
                if ((requestCount % 5 == 1) || (requestCount % 5 == 2))
                {
                    return StatusCode(500, "Simulated server error");
                }
                return Ok("Success");
            }
        }
    }
}

```

The code simulates a failure on the 2nd and 4th requests in every group of 5.

Now the fun part..


### Breakdown the circuit breaker implementation

The first file we need to look at would be the **PollyPolicy**.

```cs
public class PollyPolicy
{
    public readonly AsyncCircuitBreakerPolicy AsyncCircuitBreakerPolicy;
    public readonly AsyncNoOpPolicy AsyncNoOpPolicy;

    public PollyPolicy(IOptions<CircuitBreakerConfigurationSetings> optionsCircuitBreaker, ILogger<CircuitBreakerPolicy> logger)
    {
        var circuitBreakerSettings = optionsCircuitBreaker.Value;

        AsyncCircuitBreakerPolicy = Policy
            .Handle<ProviderException>()
            .Or<GlobalTimeoutException>()
            .AdvancedCircuitBreakerAsync(
                failureThreshold: circuitBreakerSettings.FailureThreshold,
                samplingDuration: TimeSpan.FromMilliseconds(circuitBreakerSettings.SamplingDuration),
                minimumThroughput: circuitBreakerSettings.MinimumThroughput,
                durationOfBreak: TimeSpan.FromMilliseconds(circuitBreakerSettings.DurationOfBreak),
                onBreak: (exception, duration) =>
                {
                    logger.LogError($"CIRCUIT_BREAKER_OPEN - Circuit breaker opened due to: {exception.Message}");
                },
                onHalfOpen: () =>
                {
                    logger.LogWarning("CIRCUIT_BREAKER_HALF_OPEN - Circuit breaker is half-open.");
                },
                onReset: () =>
                {
                    logger.LogInformation("CIRCUIT_BREAKER_CLOSED - Circuit breaker is closed.");
                });

        AsyncNoOpPolicy = Policy.NoOpAsync();
    }
}
```

This provides a mechanism to apply a circuit breaker for handling certain failures (e.g. ProviderException, GlobalTimeoutException).

Let's dig deeper.

Parameters:

- failureThreshold: this represents the percentage of action that must fail before the circuit breaker opens.
- samplingDuration: this is the time window over which the failure rate is measured.
- minimumThroughput: this is the minimum number of requests that must occur within the sampling duration  for the circuit breaker to open.
- durationOfBreak: this defines how long the curcuit breaker remains open before it transitions to a half-open state to test if the underlying issue is resolved.

Actions:

- onBreak: the circuit breaker is open which means any incoming requests will immediately be rejected. 
- onHalfOpen: the circuit breaker allows a limited number of requests to pass through to check if the issue has been resolved.
- onReset: the circuit breaker closes which assumes the underlying issue is resolved.


Quick one: Why do we need the circuit breaker to open?
- This is a protective measure designed to prevent further strain on a system that is already experiencing high failure rates. This is also to lessen if not avoid further administration issues from an operational standpoint.


Next, we look at the **ResilientGlobalTimeoutAdapter**.

```cs
public class ResilientGlobalTimeoutAdapter : IGlobalTimeoutAdapter
{
    private readonly AsyncCircuitBreakerPolicy _asyncCircuitBreakerPolicy;

    public ResilientGlobalTimeoutAdapter(PollyPolicy pollyPolicy)
    {
        _asyncCircuitBreakerPolicy = pollyPolicy.AsyncCircuitBreakerPolicy;
    }

    public async Task<T> ExecuteAsync<T>(Func<Task<T>> asyncMethod, CancellationToken cancellationToken)
    {
        return await _asyncCircuitBreakerPolicy.ExecuteAsync(() => ExecuteMethodAsync(asyncMethod, cancellationToken));
    }

    private async Task<T> ExecuteMethodAsync<T>(Func<Task<T>> asyncMethod, CancellationToken cancellationToken)
    {
        try
        {
            return await asyncMethod().WithCancellation(cancellationToken);
        }
        catch(OperationCanceledException operationCanceledException)
        {
            if (!cancellationToken.IsCancellationRequested)
                throw new GlobalTimeoutException("HttpClient Timed out.", "HttpClient", operationCanceledException);
            else
                throw new GlobalTimeoutException("Global Timeout reached.", "ExecuteAsync", operationCanceledException);
        }
    }
}
```

This class acts as a resilience layer that applies the circuit breaker policy to protect asynchronous operations.
If you noticed, the ProviderException isn't thrown directly in this layer. 
This would be thrown by the service/method that ExecuteAsync represents.

Now, let's just skim through the the implementation from the controller down to the service manager to the http client:

***Controller:***

This endpoint consumes the resilience layer we talked about.

```cs
[HttpPost]
public async Task<IActionResult> DoSomeStuff([FromBody] MockRequestDTO mockRequestDTO)
{
    using (_logger.BeginScope(mockRequestDTO.MockRequestId ?? string.Empty))
    {
        var cancellationTokenSource = new CancellationTokenSource();
        var token = cancellationTokenSource.Token;

        try
        {
            if (!ModelState.IsValid)
            {
                _logger.LogWarning("Invalid model state for request: {@MockRequestDTO}", mockRequestDTO);
                return BadRequest();
            }

            var mockResponseDTO = await _globalTimeoutAdapter.ExecuteAsync(() =>
                _processStuffProcessorManager.DoSomeStuff(mockRequestDTO), token);

            return Ok(new { ProviderCode = mockResponseDTO.ProviderCode });
        }
        catch (Exception ex)
        {
            _exceptionHandler.HandleException(ex, _logger);
            return StatusCode(500, ex.Message);
        }
    }
}
```

***Service Manager:***

Ideally additional business logic is implemented on this side. For the demo, we just call the httpclient right away.

```cs
public async Task<MockResponseDTO> DoSomeStuff(MockRequestDTO responseDTO)
{
    try
    {
        return await _sendRequestToExternalProviderHttpClient.SendRequestByMockRequest(responseDTO);
    }
    catch (Exception ex)
    {
        _exceptionHandler.HandleException(ex, _logger);
        throw new ProviderException("HTTP Request failed.", "HttpClient", ex);
    }
}
```

***HttpClient:***

Nothing fancy on the implementation below as this just consumes the Demo API producer that we created earlier. 

```cs
public async Task<MockResponseDTO> SendRequestByMockRequest(MockRequestDTO mockRequestDTO)
{
    if (mockRequestDTO is null)
        throw new InvalidRequestException("MockRequestDTO should not be null.");

    try
    {
        var request = Utility.BuildHttpRequest(_serviceUri, JsonConvert.SerializeObject(mockRequestDTO));

        HttpResponseMessage response = await _httpClient.SendAsync(request);

        response.EnsureSuccessStatusCode();

        var content = await response.Content.ReadAsStringAsync();

        return new MockResponseDTO
        {
            ProviderCode = content.Contains("Success", StringComparison.OrdinalIgnoreCase) ? "Success" : "ProviderError"
        };
    }
    catch (Exception ex)
    {
        _exceptionHandler.HandleException(ex, _logger);
        throw; 
    }
}
```


Lastly, let's not forget to do our dependency injection which I forgot on my repository lol
```cs
public void ConfigureServices(IServiceCollection services)
{
        services.AddMvc();
        services.AddControllers();
        services.AddLogging();
        services.AddEndpointsApiExplorer();
        services.AddSingleton<PollyPolicy>();

        services.AddSwaggerGen();
        services.AddTransient<IExceptionHandler, ExceptionHandler>();
        services.AddTransient<IGlobalTimeoutAdapter, ResilientGlobalTimeoutAdapter>();
        services.AddScoped<IHttpClientAdapter, HttpClientAdapter>();

        services.AddHttpClient<ISendRequestToExternalProviderHttpClient, SendRequestToExternalProviderHHttpClient>();

        services.AddTransient<IProcessStuffProcessorManager, ProcessStuffProcessorManager>();

        services.AddOptions();
        services.Configure<ExternalEndpointConfigurationSettings>(Configuration.GetSection("ExternalEndpointConfiguration"));
        services.Configure<CircuitBreakerConfigurationSetings>(Configuration.GetSection("CircuitBreakerConfigurationSetings"));
}
```

That's it. Easy. On to the next! :)