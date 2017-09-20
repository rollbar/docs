## Installation

Download <a href="https://github.com/rollbar/rollbar-android/releases/latest" target="_blank" rel="noopener">rollbar-android.jar</a> and place it in your Android project's `libs` directory.

Add the following line in your custom Application subclass's `onCreate()` to initialize Rollbar:

```java
Rollbar.init(this, "{{ client_access_token }}", "production");
```

Make sure your `AndroidManifest.xml` contains the `android.permission.INTERNET` permission.

## Sending Messages & Errors to Rollbar

By default the Rollbar SDK will report all uncaught exceptions to Rollbar.

To report caught exceptions, call `reportException()`:

```java
Rollbar.reportException(new Exception("Test exception")); // default level is "warning"

try {
    amount = Integer.parseInt(data);
} except (NumberFormatException e) {
    // Providing a description for this exception
    Rollbar.reportException(e, "critical", "Unexpected data from server");
}
```

To report your own messages, call `reportMessage()`:

```java
Rollbar.reportMessage("A test message", "debug"); // default level is "info"
```

For additional configuration information, see the documentation for the <a href="https://github.com/rollbar/rollbar-android " target="_blank" rel="noopener">rollbar-android</a> SDK.
