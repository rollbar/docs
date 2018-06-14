## Installation

To send errors to Rollbar from your Java application, you should use our <a href="https://github.com/rollbar/rollbar-java" target="_blank" rel="noopener">rollbar-java</a> package. 

``` java
compile('com.rollbar:rollbar-java:1.2.0')
```

## rollbar-web

If your web server is implemented as a Servlet, you can configure and enable Rollbar entirely within your `WEB-INF/web.xml` file using rollbar-web:

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

## Configuration

All configuration is done via the Config object in `rollbar-java`. You can see the interface <a href="https://github.com/rollbar/rollbar-java/blob/master/rollbar-java/src/main/java/com/rollbar/notifier/config/Config.java" target="_blank" rel="noopener">here</a>.
