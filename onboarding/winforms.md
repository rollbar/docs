## Installation

To send errors to Rollbar from your .NET application, you should use our <a href="https://github.com/rollbar/Rollbar.NET" target="_blank" rel="noopener">Rollbar.NET</a> SDK.

Install Rollbar.Net with Nuget:

```csharp
Install-Package Rollbar
```

To use inside a Winforms Application, do the following inside your main method. You'll need your project's server-side access token to initialize the Rollbar.NET SDK.

```csharp
[STAThread]
static void Main()
{
    Rollbar.Init(new RollbarConfig
    {
        AccessToken = "{{server_access_token}}",
        Environment = "production"
    });
    Application.EnableVisualStyles();
    Application.SetCompatibleTextRenderingDefault(false);

    Application.ThreadException += (sender, args) =>
    {
        Rollbar.Report(args.Exception);
    };

    AppDomain.CurrentDomain.UnhandledException += (sender, args) =>
    {
        Rollbar.Report(args.ExceptionObject as System.Exception);
    };

    Application.Run(new Form1());
}
```

Then create a global action filter:

```csharp
public class RollbarExceptionFilter : IExceptionFilter
{
    public void OnException(ExceptionContext filterContext)
    {
        if (filterContext.ExceptionHandled)
            return;

        Rollbar.Report(filterContext.Exception);
    }
}
```

and finally add it to the global filters collection:

```csharp
private static void RegisterGlobalFilters(GlobalFilterCollection filters)
{
    ...
    filters.Add(new RollbarExceptionFilter());
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