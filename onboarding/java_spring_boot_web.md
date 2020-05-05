# Installation

## Using Gradle

Add `rollbar-spring-boot-web` to the `dependencies` section in your `build.gradle`:

``` java
compile 'com.rollbar:rollbar-spring-boot-web:1.+'
```

## Using Maven

Add `rollbar-spring-boot-web` as a dependency in your `pom.xml`:

```xml
<dependency>
  <groupId>com.rollbar</groupId>
  <version>[1.0,)</version>
  <artifactId>rollbar-spring-boot-web</artifactId>
</dependency>
```

Then run `mvn install`.

# Basic Configuration

The minimal amount of code you need to use `rollbar-spring-boot` is:

To configure `rollbar-spring-boot-web` with a Java Spring Boot Web based project, add this bean into your configuration.

``` java
@Bean
public HandlerExceptionResolver rollbarExceptionResolver() {
    return new RollbarExceptionResolver(Rollbar.init(withAccessToken("<server_access_token>").build()));
}
```

Now any exceptions created from your java spring web app, will automatically be reported to Rollbar.
