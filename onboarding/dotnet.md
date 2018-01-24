## Installation

To send errors to Rollbar from your .NET application, you should use our <a href="https://github.com/rollbar/Rollbar.NET" target="_blank" rel="noopener">Rollbar.NET</a> SDK.

Install Rollbar.Net with Nuget:

```csharp
Install-Package Rollbar
```

## Send a Message

You'll need your project's server-side access token to initialize the Rollbar.NET SDK. Sending
a message to the Rollbar server is as simple as:

```csharp
RollbarLocator.RollbarInstance.Configure(new RollbarConfig("POST_SERVER_ITEM_ACCESS_TOKEN"))
RollbarLocator.RollbarInstance.Info("Rollbar is configured properly.")
```

A few seconds after you execute this code, the message should appear on your project's "Items" page.


## Report an Error

To send an error, rather than a message, execute the following code after initializing Rollbar:

```csharp
try
{
    int value = 1 / int.Parse("0");
}
catch (System.Exception ex)
{
    RollbarLocator.RollbarInstance.Error(Exception);
}
```

A few seconds after you execute this code, an exception should appear on your project's "Items" page.
This item will include the basic exception information and a stack trace, along with the values of
local variables and the arguments passed to each function at each frame in the stack trace.

## Add Rollbar to Your .NET Application

Once you've verified that the Rollbar SDK is configured correctly and can communicate with the Rollbar server, you'll
want to add the SDK to your existing applications. See the Rollbar.NET docs <a href="https://rollbar.com/docs/notifier/rollbar.net/" target="_blank" rel="noopener">here</a> for further information.