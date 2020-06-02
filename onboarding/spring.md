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
package com.example.app;   // Set this to your project package

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
    "com.example.app",    // Set this to your project package
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


# Further Configuration and Java Docs

If you are interested in learning more about how to configure Rollbar you can reference the doc <a href="https://docs.rollbar.com/docs/spring#configure-the-rollbar-bean" target="_blank" rel="noopener">here</a>. Also our Java Docs are available <a href="https://javadoc.io/doc/com.rollbar" target="_blank" rel="noopener">here</a>.


***
