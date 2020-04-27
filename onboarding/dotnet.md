## Installation instructions for any .NET compatible application

To send errors to Rollbar from your .NET application, you should use our <a href=“https://github.com/rollbar/Rollbar.NET” target=“_blank” rel=“noopener”>Rollbar.NET</a> SDK.

Install Rollbar.Net with Nuget:

```csharp
Install-Package Rollbar
```

## Send a Message

You’ll need your project’s server-side access token to initialize the Rollbar.NET SDK. Sending
a message to the Rollbar server is as simple as:

```csharp
RollbarLocator.RollbarInstance.Configure(new RollbarConfig(“{{ server_access_token }}“));
RollbarLocator.RollbarInstance.Info(“Rollbar is configured properly.“);
```

A few seconds after you execute this code, the message should appear on your project’s “Items” page.

## Report an Error

To send an error, rather than a message, execute the following code after initializing Rollbar:

```csharp
try
{
    int value = 1 / int.Parse(“0");
}
catch (System.Exception ex)
{
    RollbarLocator.RollbarInstance.Error(ex);
}
```

A few seconds after you execute this code, an exception should appear on your project’s “Items” page.
This item will include the basic exception information and a stack trace, along with the values of
local variables and the arguments passed to each function at each frame in the stack trace.

# Integrating the SDK into a Specific .NET compatible Application Framework

Once you’ve verified that the Rollbar SDK is configured correctly and can communicate with the Rollbar server, you’ll
want to add the SDK to your existing applications based on your application development framework. To gain a better 
understanding of the intended usage patterns for the SDK, see the Rollbar.NET docs <a href=“https://docs.rollbar.com/docs/dotnet” target=“_blank” rel=“noopener”>here</a> for further information.

Here is the list of documentation article we recommend reviewing before making attempts to properly integrate into a real application:

- <a href=“https://docs.rollbar.com/docs/dotnet” target=“_blank” rel=“noopener”>SDK Introduction</a>
- <a href=“https://docs.rollbar.com/docs/overview” target=“_blank” rel=“noopener”>SDK Components Overview</a>
- <a href=“https://docs.rollbar.com/docs/basic-usage” target=“_blank” rel=“noopener”>Basic Logger/Notifier Usage Scenarios</a>
- <a href=“https://docs.rollbar.com/docs/logger-configuration” target=“_blank” rel=“noopener”>Logger’s Configuration Options/Alternatives</a>
- <a href=“https://docs.rollbar.com/docs/more-advanced-logger-usages” target=“_blank” rel=“noopener”>More Advanced Usage Scenarios</a>
- <a href=“https:https://github.com/rollbar/Rollbar.NET/tree/master/Samples” target=“_blank” rel=“noopener”>Also, review a repo of our application/technology integration samples</a>

Good luck and have fun rolling your product quality bar even higher!
