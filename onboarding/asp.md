## Installation

To send errors to Rollbar from your .NET application, you should use our <a href="https://github.com/rollbar/Rollbar.NET" target="_blank" rel="noopener">Rollbar.NET</a> SDK.

Install Rollbar.Net with Nuget:

```csharp
Install-Package Rollbar
```

To use inside an ASP.Net Application, first in your global.asax.cs and Application_Start method initialize Rollbar:

```csharp
protected void Application_Start()
{
    ...
    Rollbar.Init(new RollbarConfig
    {
        AccessToken = ConfigurationManager.AppSettings["{{server_access_token}}"],
        Environment = ConfigurationManager.AppSettings["Rollbar.Environment"]
    });
    ...
}
```

## Send a Message

Sending a message to the Rollbar server is as simple as running this command after initializing Rollbar:

```csharp
Rollbar.Report("Rollbar is configured correctly");
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
    Rollbar.Report(ex);
}
```

A few seconds after you execute this code, an exception should appear on your project's "Items" page.
This item will include the basic exception information and a stack trace, along with the values of
local variables and the arguments passed to each function at each frame in the stack trace.

## Add Rollbar to Your .NET Application

Once you've verified that the Rollbar SDK is configured correctly and can communicate with the Rollbar server, you'll
want to add the SDK to your existing applications. See the Rollbar.NET docs <a href="https://rollbar.com/docs/notifier/rollbar.net/" target="_blank" rel="noopener">here</a> for further information.