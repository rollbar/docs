## Installation

To send errors to Rollbar from your Java application, you should use our <a href="https://github.com/rollbar/rollbar-java" target="_blank" rel="noopener">java-rollbar</a> notifier library. 

You can, of course, build it yourself and depend on the .jar manually, however, the modules are up on maven central and can be installed in most tool chains pretty trivially. 

### Maven

All of these can be installed as Maven projects. Simply add the dependency to your pom file:

```xml
<dependencies>
<dependency>
  <groupId>com.rollbar</groupId>
   <artifactId>rollbar</artifactId>
   <version>0.5.3</version>
</dependency>
</dependencies>
```

### Gradle

```groovy
compile('com.rollbar:rollbar:0.5.3')
```

## Usage

For actual usage, the easiest way to get started is with the `rollbar` package. See the <a href="https://github.com/rollbar/rollbar-java/tree/master/rollbar" target="_blank" rel="noopener">documentation there</a>.

## Contributing

This library was written by someone who knows C# much better than Java. Feel free to issue stylistic PRs, or offer
suggestions on how we can improve this library.

1. <a href="https://github.com/rollbar/rollbar-java" target="_blank" rel="noopener">Fork it</a>
2. Create your feature branch (```git checkout -b my-new-feature```).
3. Commit your changes (```git commit -am 'Added some feature'```)
4. Push to the branch (```git push origin my-new-feature```)
5. Create new Pull Request

