---
layout: post
permalink: "/post/software-engineering/circuit-breaker-p1"
title:  "Software Resilience with Circuit Breaker"
subtitle: "Foundations (1/2)"
date:   2023-11-17 01:02:19 +1100
categories: [Software Engineering, Architecture]
tags: [Circuit Breaker, Resilience, .NET, Polly, Microservices, Best Practices]
article-series:
  id: "circuit-breaker-series"
  series-title: "Building Resilient Software with Circuit Breaker"
  sidebar-label: "Foundations"
  part: 1
  total: 2
---

Hey there! It's been a while..
<br/>
<br/>
If you're working on the technical side which navigates the complex landscape of integration, seeking a refresher on software resiliency, or perhaps eager to implement the Circuit Breaker pattern, then this blog is for you..
<br/>
If you're on the business side that wants to ensure a smooth sailing even in the face of disruptions, then keep on reading!
<br/>

### Intro to Software Resiliency

In the dynamic world of software, disruptions are inevitable.

Software resiliency is the key to minimizing downtime and ensuring seamless operations. 
<br/>It acts as a safety net, allowing systems to adapt, recover, and continue functioning even in the face of unexpected failures.
<br/>
By embracing resiliency, organizations safeguard user experiences, maintain business continuity, and solidify digital infrastructure against the unpredictable aspects of the digital landscape.

Why is there a crucial need for software resiliency?
<br/>
Well, let's try to imagine a common scenarios that unexpectedly happens:
1. E-commerce downtime
    - An online retail platform experiences server issues during a major sales event, resulting in transaction failures.
        - This will result in revenue loss and customer dissatisfaction.
2. Financial System Outage
    - A financial organization undergoes an unexpected disruption, causing temporary unavailability of online services.
        - This will disrupt financial transactions, access to funds/investments, etc..
3. Travel Reservation System Failure
    - A global airline carrier's reservation system encounters a glitch, leading to double bookings or cancellations.
        - This will result in revenue loss and most likely damage the company's reputation.

You don't want to be on both ends if these scenarios happen..

If you're still not sold, take note that in the ever-evolving landscape of technology, the importance of software resiliency cannot be overstated.
<br/><br/> *There is no such thing as a perfect software!*
<br/><br/> Businesses relying heavily on digital systems continuosly encounter challenges, and software failures can have profound implications.
<br/>

### Different Types of Integration

Let's see a few:

 - Point-to-Point Integration: Establishes a direct connection between two systems, allowing them to communicate seamlessly.
 - Hub and Spoke Integration: Utilizes a centralized hub that connects multiple systems independently.
 - Enterprise Service Bus: Deploys a centralized platform managing communication that supports various protocols.
 - Microservices Integration Integration: Consists of autonomous services communicating via APIs within a flexible and agile environment.
 - Data Integration: Combines and presents data from different sources for a unified view.
 - API Integration: Enables different software applications to communicate through defined APIs.
 - Cloud Integration: Connects on-prem systems with cloud-based services, ensuring seamless data flow.
 - B2B Integration: Facilitates communication and data exchange between different businesses.
 
Whether you're working on any of the list above, this is the time to push for software resiliency.

Still not sold? Well, you might encounter these challenges and it's time to reconsider:
- Handling Service Failures
- Dealing with Unpredictable Workloads
- Ensuring Fault Tolerance
- Balancing Redundancy and Efficiency
- Ensuring Timely Incident Detection and Response
- Adapating to Changing Environments
- Balancing Consistency and Availability 

If you're still not sold, then you can rely on pure dumb luck hoping you don't encounter the above challenges :)

### Circuit Breaker Pattern

What is circuit breaker pattern and how is it relevant to software resiliency?
<br/> Well, this pattern stands as a crucial safeguard that serves as a protective mechanism which is designed to enhance the resilience of software applications when integrating with external services or components.

#### Key Components
1. Closed State
    - In normal operation, the Circuit Breaker remains in a *closed* state, allowing requests to flow seamlessly through.
2. Open State
    - When a predefined threshold of failures or disruptions is crossed, the Circuit Breaker transitions to an *open* state.
        - During this state, it blocks any further requests from reaching the problematic component which prevents potential damage.
3. Half-Open State
    - After a specified time in the "open" state, the Circuit Breaker transitions to a *half-open* state. 
        - This will allow a limited number of requests to pass through to assess whether the underlying component has recovered.

#### Roles and Benefits

- Failure Prevention
    - The Circuit Breaker pattern acts as a shield, proactively preventing a system from sending requests to an already-failing or degraded component. 
        - This helps to conserve resources and avoid making the problem worse.
- Resilience Enhancement
    -  Instead of continuously trying to interact with a malfunctioning component, it provides a controlled way to *pause* communication until the issue is resolved.
        - This enables applications become more resilient to temporary failures.
- Adaptive Systems
    - When disruptions occur, it provides a graceful and controlled response, promoting the overall stability of the application
        - This provide applications to dynamically adjust to changing conditions.

<br/>
Still find it hard to believe?
<br/>
<br/>
Imagine a home without a circuit breaker..
<br/>
Now unexpectedly, a power surge occurs. What happens next?
<br/>
The excess electrical current flows unchecked through your home's wiring which can lead to overheating that damages appliances, electronic devices, and potentially causing electrical fires.
<br/><br/>
Without the protective mechanism of a circuit breaker, the entire electrical system is vulnerable to extensive and uncontrolled damage during power surges.


Circuit Breaker Libraries for **.NET**
1. Polly - "a .NET resilience and transient-fault-handling library that allows developers to express resilience strategies such as Retry, Circuit Breaker, Hedging, Timeout, Rate Limiter and Fallback in a fluent and thread-safe manner."
    - Checkout their <a href="https://github.com/App-vNext/Polly">github</a>
2. Steeltoe Circuit Breaker - part of the steeltoe project which extends for the .NET platform. 
    - Checkout their <a href="https://github.com/SteeltoeOSS/Steeltoe">github</a> and for the circuit breaker <a href="https://github.com/SteeltoeOSS/CircuitBreaker">guide</a>
3. Hystrix.Dotnet - "A combination of circuit breaker and timeout. The .NET version of the open source Hystrix library built by Netflix."
    - Checkout their <a href="https://github.com/Travix-International/Hystrix.Dotnet">github</a>
4. Not really a library but a reference from <a href="https://learn.microsoft.com/en-us/dotnet/architecture/microservices/implement-resilient-applications/implement-circuit-breaker-pattern">Microsoft docs</a> which uses IHttpClientFactory and Polly.

#### What's Next?

In the next part, I will show you a quick demo and deep dive into the working example.
For the meantime, if you're keen to see a base implementation, you can checkout  <a href="https://github.com/vaughnellis/circuit-breaker-design-pattern/tree/master">my public repo</a>. <br/>
Take note that it does not have a README due to my laziness but I will be using and extending this for the demo.

Stay tuned!