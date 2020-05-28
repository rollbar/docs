# Installation

** WORKING DRAFT **

## Using Gradle

Add the necessary dependency based on your project type.

### Spring Boot

For Spring Boot add the following to the `dependencies` section in your `build.gradle`: 

``` java
compile 'com.rollbar:rollbar-spring-boot-webmvc:1.+'
```

### Spring Web MVC

For Spring Web MVC add the following to the `dependencies` section in your `build.gradle`: 

``` java
compile 'com.rollbar:rollbar-spring-webmvc:1.+'
```


# Basic Configuration

- Create a configuration class that has a component scan on `com.rollbar.spring` along with your project package 
namespace. 
- Set your access token


``` java
@Configuration()
@EnableWebMvc
@ComponentScan({
    "Your project package namespace", // set your project namespace here
    "com.rollbar.spring"
})
public class RollbarConfig {

  /**
   * Register a Rollbar bean to configure App with Rollbar.
   */
  @Bean
  public Rollbar rollbar() {
    return new Rollbar(getRollbarConfigs("<ACCESS TOKEN>"));
  }

  private Config getRollbarConfigs(String accessToken) {

    // Reference ConfigBuilder.java for all the properties you can set for Rollbar
    return RollbarSpringConfigBuilder.withAccessToken(accessToken)
            .environment("development")
            .build();
  }
}
```
