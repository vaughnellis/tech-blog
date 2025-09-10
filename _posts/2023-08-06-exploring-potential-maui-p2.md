---
layout: post
permalink: "/post/software-engineering/exploring-the-potential-of-net-maui-p2"
title:  "Exploring the Potential of .NET MAUI"
subtitle: Demo
date:   2023-07-09 07:24:19 +1100
reading_time: 6
categories: [Software Engineering, Mobile Development]
tags: [.NET MAUI, Cross-Platform, Xamarin, Mobile Development, C#, XAML, SignalR]
series:
  id: "net-maui-series"
  title: "Exploring .NET MAUI"
  part: 2
  total: 2
---
Hey there, let's continue where we left off.

This is what we wanted to achieve
![MAUI](/assets/dotnet-maui-demo-p2.gif)

<br/>

### Provision SignalR service in Azure

This should be straightforward.
All you need to fill up are the details below:
- Subscription
- Resource Group Name
- Region
- Pricing Tier
- Unit count
- Service Mode

To test it out, default configuration will do for now.

### Configure and Implement SignalR communication in our .NET MAUI App

We will need to install the ***Microsoft.AspNetCore.SignalR.Client*** library in our MAUI App template.

Once done, let's go to our MessagingApp.xaml.cs.
We need to perform the following actions:

- Declare a property for the Hub Client.

```c#
private readonly HubConnection _connection;
```

- Setting up the SignalR Connection

```c#
 _connection = new HubConnectionBuilder()
            .WithUrl("http://domain/hub") // Your domain/IP address and Hub name goes here
            .Build();
```

- Setting up the callback for the Render the *MessageReceived* event andd Render updates whenever a message has been published

```c#
  _connection.On<string>("MessageReceived", async (message) =>
        {
            await MainThread.InvokeOnMainThreadAsync(() =>
            {
                // Update the UI with the received message
                 UpdateMessageUI(message);
            });
            
        });
```

- Start a background task to establish the SignalR connection

```c#
  Task.Run(() =>
        {
            Dispatcher.Dispatch(async () =>
                await _connection.StartAsync());
        });
```

We will also need to refactor *OnSendMessageClicked* with the code below:

```c#
 string message = MessageEntry.Text;

        await _connection.InvokeCoreAsync("SendMessage", args: new[] { MessageEntry.Text });

        // Clear the message entry
        MessageEntry.Text = String.Empty;
```

This will send the message from the client to the server-side SignalR hub.

For the *UpdateMessageUI* implementation, use the code snippet below:

 ```c#
        // Create a new StackLayout to hold the message and icon
        StackLayout messageLayout = new StackLayout
        {
            Orientation = StackOrientation.Horizontal,
            HorizontalOptions = LayoutOptions.Start,
            Spacing = 10
        };

        // Create an Image for the icon (replace "icon.png" with your icon's image source)
        Image iconImage = new Image
        {
            Source = "messagingIcon.jpg",
            HeightRequest = 40,
            WidthRequest = 40,
            Aspect = Aspect.AspectFill
        };

        // Create a Frame to contain the Label with a rounded background
        Frame messageFrame = new Frame
        {
            BackgroundColor = Color.FromRgb(211, 211, 211), // Use
            Padding = new Thickness(10),
            CornerRadius = 10, // Set the corner radius for a round shape
            Content = new Label
            {
                Text = message,
                HorizontalOptions = LayoutOptions.Start,
                VerticalOptions = LayoutOptions.Center
            }
        };

        // Determine the message alignment based on the even/odd index
        if (MessageStackLayout.Children.Count % 2 == 0)
        {
            // For even indexes, align the message to the right
            messageLayout.HorizontalOptions = LayoutOptions.End;
            messageLayout.Children.Add(messageFrame);
            messageLayout.Children.Add(iconImage);
        }
        else
        {
            // For odd indexes, align the message to the left
            messageLayout.Children.Add(iconImage);
            messageLayout.Children.Add(messageFrame);
        }

        // Add the messageLayout to the MessageStackLayout
        MessageStackLayout.Children.Add(messageLayout);
 ```
<br/>

### Define server-side SignalR Hub

We will need to create a new empty Web API project in our solution.
After creating the new project, we will need to install the **Microsoft.AspNetCore.SignalR** library.

- Define Server-Side SignalR Hub Implementation

Create a new class and name it *ChatHub* and inherit *Hub* class from *Microsoft.AspNetCore.SignalR*:

Afterwards, add the function below:

 ```c#
   public async Task SendMessage(string message)
        {
            Console.WriteLine("Message Published: " + message);
            await Clients.All.SendAsync("MessageReceived", message);
        }
 ```

 - Enable SignalR 

 On the *Program.cs*, add the following code snippet below:

  ```c#
    builder.Services.AddSignalR();
    app.MapHub<ChatHub>("/chat");
   ```
This is for adding SignalR services to the app's dependency injection container and to map/configure a SignalR hub endpoint to a URL route.

<br/>

### Testing it out

After everything has been said and done, you can now run the MAUI App template project. <br/>
Once it is running, you can start a new instance for the server-side project.