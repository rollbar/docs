## Installation With <a href="http://cocoapods.org/" target="_blank" rel="noopener">Cocoapods</a> 
_**NOTE:** This is our recommended installation method._

In your Podfile:

```
platform :ios

target 'YOUR_APP_NAME' do
  pod "Rollbar", "~> 1.0.0-alpha11"
end
```
**NOTE:** The `plaftform:ios` statement is required 


### Without Cocoapods

1. Download the `Rollbar.zip` file from the <a href="https://github.com/rollbar/rollbar-ios/releases/latest/" target="_blank" rel="noopener">latest release of rollbar-ios</a>.

2. Extract the Rollbar directory in the zip file to your Xcode project directory.

3. In Xcode, select _File_ -> _Add Files to "[your project name]"_ and choose the Rollbar directory from step 2.

## Configuration and Testing

In your `AppDelegate.m` file, add the following import statement:

```objectivec
#import <Rollbar/Rollbar.h>
```

Then add the following to `application:didFinishLaunchingWithOptions:`:

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    [Rollbar initWithAccessToken:@"{{client_access_token}}"];
    [Rollbar infoWithMessage:@"Test message"];
    // Rest of your code here...
    return YES;
}
```

Once you've confirmed that a test message was sent to your Rollbar project, remove the call to `[Rollbar infoWithMessage]`.

## Further Configuration

For additional configuration instructsion, including instructions for symbolication, see the documentation for <a href="https://rollbar.com/docs/notifier/rollbar-ios" target="_blank" rel="noopener">rollbar-ios</a>.
