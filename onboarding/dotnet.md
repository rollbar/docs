## Installation instructions for any .NET compatible application

To send errors to Rollbar from your .NET application, you should use our [Rollbar.NET SDK](https://github.com/rollbar/Rollbar.NET).

Install Rollbar .Net with Nuget:

```csharp
Install-Package Rollbar
```

## Send a Message

You’ll need your project’s server-side access token to initialize the Rollbar .NET SDK. Sending
a message to the Rollbar server is as simple as:

```csharp
RollbarLocator.RollbarInstance.Configure(new RollbarConfig("{{ server_access_token }}"));
RollbarLocator.RollbarInstance.Info("Rollbar is configured properly.");
```

A few seconds after you execute this code, the message should appear on your project’s Items page.

## Report an Error

To send an error, rather than a message, execute the following code after initializing Rollbar:

```csharp
try
{
    int value = 1 / int.Parse("0");
}
catch (System.Exception ex)
{
    RollbarLocator.RollbarInstance.AsBlockingLogger(TimeSpan.FromSeconds(1)).Error(ex);
}
```

A few seconds after you execute this code, an exception should appear on your project’s Items page.
This item will include the basic exception information and its stack trace.

# Integrating the SDK into a Specific .NET compatible Application Framework

Once you’ve verified that the Rollbar SDK is configured correctly and can communicate with the Rollbar server, you’ll
want to add the SDK to your existing applications based on your application development framework. To gain a better 
understanding of the intended usage patterns for the SDK, see the Rollbar .NET docs [here](https://docs.rollbar.com/docs/dotnet) for further information.

Here is the list of articles from our docs we recommend reviewing before making attempts to fully integrate into a complete application:

- [SDK Introduction](https://docs.rollbar.com/docs/dotnet)
- [SDK Components Overview](https://docs.rollbar.com/docs/overview)
- [Basic Logger/Notifier Usage Scenarios](https://docs.rollbar.com/docs/basic-usage)
- [Logger’s Configuration Options/Alternatives](https://docs.rollbar.com/docs/logger-configuration)
- [More Advanced Usage Scenarios](https://docs.rollbar.com/docs/more-advanced-logger-usages)
- To better integrate the SDK into a specific application type or existing logging framework look for suitable documentation article titled as “Integrating as/with ...“. Pick the one that matches best your desired integration strategy.
- [Also, review a repo of our application/technology integration samples](https://github.com/rollbar/Rollbar.NET/tree/master/Samples)


Good luck and have fun rolling your product quality bar even higher!
