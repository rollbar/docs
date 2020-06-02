# Follow these steps

Send your first event and start using Rollbar with three easy steps with your Spring project! 

<br />

## Step 1: Install Rollbar 

Depending on your project type, add the appropriate dependency for gradle.

<br />


**Spring Boot**

If you have a Spring Boot project add the following to your `dependencies` section in your `build.gradle`:
 
``` java
compile 'com.rollbar:rollbar-spring-boot-webmvc:1.7.2'
```

<br />


**Spring Web MVC**

For a Spring Web MVC project add the following to the `dependencies` section in your `build.gradle`: 

``` java
compile 'com.rollbar:rollbar-spring-webmvc:1.7.2'
```

<br />

## Step 2: Configure Rollbar

**Basic Rollbar Configuration**
1. Create a new class `RollbarConfig.java` in your project
2. Copy the sample code below into  `RollbarConfig.java`
3. Ensure `com.example.app` is set to your project namespace

After adding this configuration in to your Spring project, all exceptions raised by Spring will now be sent into Rollbar.

``` java
package com.example.app;                     // Don't forget to update

import com.rollbar.notifier.Rollbar;
import com.rollbar.notifier.config.Config;
import com.rollbar.spring.webmvc.RollbarSpringConfigBuilder;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;


@Configuration()
@EnableWebMvc
@ComponentScan({
    "com.example.app",                        // Don't forget to update
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

<br />

## Step 3: Verify your configuration

You can verify your configuration by sending us a test messing. Using the `rollbar` instance, you can send Rollbar a test with the example code below. On success this screen will refresh, your test will be visible and you can start using Rollbar!


``` java

// Sends a debug message to your Spring project on Rollbar
rollbar.debug("Here is some debug message");

```

<br />


# Further Configuration and Java Docs

If you are interested in learning more about how to configure Rollbar you can reference the doc <a href="https://docs.rollbar.com/docs/spring#configure-the-rollbar-bean" target="_blank" rel="noopener">here</a>. Also our Java Docs are available <a href="https://javadoc.io/doc/com.rollbar" target="_blank" rel="noopener">here</a>.


***
