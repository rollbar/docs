<div class="alert alert-info">
	Rollbar's React Native SDK is currently a <code>beta</code> release.  For details, please see the <a href="https://github.com/rollbar/rollbar-react-native/blob/master/README.md">Readme</a>.<br>
	To report issues, make suggestions, or ask questions, please <a href="https://github.com/rollbar/rollbar-react-native/issues/new">create an issue in Github</a>.
</div>

## Installation

Integrating requires the following steps:


1. Install the package from NPM

```
$ npm install rollbar-react-native --save
```

or

```
$ yarn add rollbar-react-native
```

2. Link the native modules with the underlying project:

```
$ react-native link rollbar-react-native
```

3. For iOS, download the Rollbar iOS Framework
   [here](https://github.com/rollbar/rollbar-ios/releases/download/v1.0.0-alpha5/Rollbar.zip). Extract this
   zip file somewhere. You will need it for the next couple steps.

4. Open the underlying Xcode project for your app:

```
$ open ios/MyAwesomeApp.xcodeproj
```

5. Drag the framework from the extracted zip file to be part of the `RollbarReactNative` project:

![](https://raw.githubusercontent.com/rollbar/rollbar-react-native/master/iosFrameworks.png)

We recommend checking the box that says "Copy items if needed". If you are managing your vendored
dependencies in some other way where you do not want to check that box, then I presume you know what
you are doing.

### Cocoapods

We currently do not recommend using Cocoapods for integrating with Rollbar. This is being worked on,
but at the moment the following instructions may or may not work.

If you are using Cocoapods, then you need to add the following to your pod file:

```
pod 'React', path: '../node_modules/react-native'
pod 'RollbarReactNative', path: '../node_modules/rollbar-react-native/ios'
```

and depending on your version of React Native, you will also need:

```
pod 'yoga', path: '../node_modules/react-native/ReactCommon/yoga'
```

Then perform a `pod install`.

You also need to ensure the static library is linked with your app in the generated workspace like
all other Cocoapods dependencies.

## Configuration

### Javascript

In both `index.ios.js` and `index.android.js` you need to instantiate a Rollbar Client:

```js
import { Client } from 'rollbar-react-native'
const rollbar = new Client('{{ client_access_token }}');
```

### iOS

In `AppDelegate.m` you need to import `RollbarReactNative`

```objc
#import <RollbarReactNative/RollbarReactNative.h>
```

and initialize it

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
{
  [RollbarReactNative initWithAccessToken:@"{{ client_access_token }}"];
  ...
}
```

The interface for `RollbarReactNative` in native iOS code is the same as
https://github.com/rollbar/rollbar-ios. Crashes in native code will be reported automatically on the
next app launch.

### Android

We require minSdkVersion of at least 19 be set in your app/build.gradle file.

In `MainApplication.java` you need to import `RollbarReactNative`

```java
import com.rollbar.RollbarReactNative;
```

and initialize it

```java
@Override
public void onCreate() {
  super.onCreate();
  RollbarReactNative.init(this, "{{ client_access_token }}", "production");
  ...
}
```

The interface for `RollbarReactNative` in native Android code is the same as the rollbar-android
part of [rollbar-java](https://github.com/rollbar/rollbar-java). Crashes in native code will be reported
automatically on the next app launch.

## Send a message

After instantiating Rollbar in both `index.ios.js` and `index.android.js` as shown above, simply call:

```js
rollbar.log('Hello world!');
```

A few seconds after you execute this code, the message should appear on your project's "Items" page.


Once you've verified that the Rollbar SDK is configured correctly and can communicate with the Rollbar server, you'll
want to check out additional configuration options and further instructions. Check out the docs [here](https://rollbar.com/docs/notifier/rollbar-react-native/).