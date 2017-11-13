<div class="alert alert-info">
    Rollbar's Java SDK is currently a <code>beta</code> release.  For details, please see the <a href="https://github.com/rollbar/rollbar-java/blob/master/README.md">Readme</a>.<br>
    To report issues, make suggestions, or ask questions, please <a href="https://github.com/rollbar/rollbar-java/issues/new">create an issue in Github</a>.
    </div>

## Installation

To send errors to Rollbar from your Java application, you should use our <a href="https://github.com/rollbar/rollbar-java" target="_blank" rel="noopener">rollbar-java</a> package. 

``` java
compile('com.rollbar:rollbar-java:1.0.0-beta-3')
```

There are three different entry points for using our Java libraries. The lowest level and most flexible is `rollbar-java`. If you are building a web server or an Android app, you can use `rollbar-java` directly, but we recommend using our more specific packages which take care of some of the basic plumbing for you. These packages are `rollbar-web` and `rollbar-android`, which are discussed below.

## rollbar-java

The minimal amount of code you need to use `rollbar-java` is:

``` java
import static com.rollbar.notifier.config.ConfigBuilder.withAccessToken;
import com.rollbar.notifier.Rollbar;
Rollbar rollbar = Rollbar.init(withAccessToken("{{ server_access_token }}"));
rollbar.log("Hello, Rollbar");
```

A few seconds after you execute this code, the message should appear on your project's "Items" page.

For a more detailed example integration, see below: 

We initialize `com.rollbar.notifier.Rollbar` with a `Config` which has the access token and other configuration properties set on it.
We can then this this instance of Rollbar to report messages via the `log/debug/warning/error/critical` methods.

Any uncaught exceptions are automatically reported to Rollbar. This behavior can be turned off via the configuration.

``` java
import static com.rollbar.notifier.config.ConfigBuilder.withAccessToken;
import com.rollbar.notifier.Rollbar;
import com.rollbar.notifier.config.Config;

public class Application {
  private Rollbar rollbar;

  public Application() {
    Config config = withAccessToken("{{ server_access_token }}")
        .environment("development")
        .codeVersion("1.0.0")
        .build();
    this.rollbar = Rollbar.init(config);
  }

  public static void main(String[] args) {
    Application app = new Application();
    app.execute();
  }

  private void execute() {
    try {
      throw new RuntimeException("Some error");
    } catch (Exception e) {
      rollbar.error(e, "Hello, Rollbar");
    }
  }
}
```

A more full-featured example can be found <a href="https://github.com/rollbar/rollbar-java/tree/master/examples/rollbar-java" target="_blank" rel="noopener">on GitHub</a>. 

## rollbar-web

If your web server is implemented as a Servlet, you can configure and enable Rollbar entirely within your `WEB-INF/web.xml` file:

``` java
<?xml version="1.0" encoding="UTF-8"?>
<web-app ...>
    <!-- Rollbar listener and filter -->
    <listener>
        <listener-class>com.rollbar.web.listener.RollbarRequestListener</listener-class>
    </listener>

    <filter>
        <filter-name>Rollbar Filter</filter-name>
        <filter-class>com.rollbar.web.filter.RollbarFilter</filter-class>
        <init-param>
            <param-name>access_token</param-name>
            <param-value>[{{ server_access_token }}]</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>Rollbar Filter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!-- Servlets -->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.yourdomain.yourapp.servlet.HelloRollbarServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
</web-app>
```

`rollbar-web` exposes a request listener and a filter which can be used to report all errors that occur during the request lifecycle to Rollbar. You can see a rollbar-web example <a href="https://github.com/rollbar/rollbar-java/tree/master/examples/rollbar-web" target="_blank" rel="noopener">on GitHub</a>.


## rollbar-android

For an Android app, we have some more specific pieces which allow you to capture more information about the Android environment automatically than what you would have to do with `rollbar-java` directly.

Set your access token in your AndroidManifest.xml file:

``` java
<?xml version="1.0" encoding="utf-8"?>
<manifest ...>
    <application ...>
        ...
        <meta-data android:name="com.rollbar.android.ACCESS_TOKEN"
        android:value="{{ client_access_token }}" />
    </application>
</manifest>
```

Then initialize Rollbar in your MainActivity:

``` java
import com.rollbar.android.Rollbar

public class MainActivity extends AppCompatActivity {

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Rollbar.init(this);
    ...
  }
}
```

You can then make direct calls to Rollbar via the managed instance:

``` java
void clickAction() {
  Rollbar.instance().log("Some button was clicked");
}
```

All uncaught exceptions which cause a crash will also be logged by Rollbar, but will not be sent until the next time the app runs.

You can see a rollbar-android example <a href="https://github.com/rollbar/rollbar-java/tree/master/examples/rollbar-android" target="_blank" rel="noopener">on GitHub</a>.


## Configuration

All configuration is done via the Config object in `rollbar-java`. You can see the interface <a href="https://github.com/rollbar/rollbar-java/blob/master/rollbar-java/src/main/java/com/rollbar/notifier/config/Config.java" target="_blank" rel="noopener">here</a>.
