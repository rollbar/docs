# Installation

Follow these steps to get your first event sent and start using Rollbar now with your Spring project! 

## Step 1: Install Rollbar 

### Configure Gradle dependencies

Depending on your project type, add the appropriate dependency for gradle.

#### Spring Boot

If you have a Spring Boot project add the following to your `dependencies` section in your `build.gradle`:
 
``` java
compile 'com.rollbar:rollbar-spring-boot-webmvc:1.7.2'
```

#### Spring Web MVC

For a Spring Web MVC project add the following to the `dependencies` section in your `build.gradle`: 

``` java
compile 'com.rollbar:rollbar-spring-webmvc:1.7.2'
```


## Step 2: Configure Rollbar

For a very simple configuration you can create a new `RollbarConfig.java` file and add it to your project. Make sure to also set `@ComponentScan` with your project package namespace.


``` java
@Configuration()
@EnableWebMvc
@ComponentScan({
    "YOUR_PROJECT_NAMESPACE", // set your project namespace here e.g., com.my.project.example
    "com.rollbar.spring"
})
public class RollbarConfig {

  /**
   * Register a Rollbar bean to configure App with Rollbar.
   */
  @Bean
  public Rollbar rollbar() {
    return new Rollbar(getRollbarConfigs("{{ server_access_token }}"));
  }

  private Config getRollbarConfigs(String accessToken) {

    // Reference ConfigBuilder.java for all the properties you can set for Rollbar
    return RollbarSpringConfigBuilder.withAccessToken(accessToken)
            .environment("development")
            .build();
  }
}
```

After adding this configuration in to your Spring project, all exceptions raised by Spring will now be sent into Rollbar.


## Step 3: Verify your configuration

You can test this by sending us a debug message now.

``` java
rollbar.debug("Here is some debug message");

```

Once you do, this screen will refresh automatically once successful. After that you are ready to start using Rollbar!


# Further Configuration

All configuration is done via the Config object in `rollbar-java`. You can see the interface <a href="https://github.com/rollbar/rollbar-java/blob/master/rollbar-java/src/main/java/com/rollbar/notifier/config/Config.java" target="_blank" rel="noopener">here</a>.

