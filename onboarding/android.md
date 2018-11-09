# Installation

## Using Android Studio or Gradle

Add the following to your **Module Gradle Settings**, usually found at `<project_dir>/app/build.gradle`:

``` java
dependencies {
    implementation 'com.rollbar:rollbar-java:1.+'
    implementation 'com.rollbar:rollbar-android:1.+@aar'
    //Rest of your dependencies...
}
```

Don't forget to run **Tools→Android→Sync Project with Gradle Files** after updating `build.gradle`.

## Using Maven

Add `rollbar-android` as a dependency in your `pom.xml`:

```xml
<dependency>
    <groupId>com.rollbar</groupId>
    <artifactId>rollbar-android</artifactId>
</dependency>
```

# Basic Configuration

Set your access token in your `AndroidManifest.xml` file:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<manifest ...>
    <application ...>
        ...
        <meta-data android:name="com.rollbar.android.ACCESS_TOKEN"
        android:value="{{ client_access_token }}" />
    </application>
</manifest>
```

Then initialize Rollbar in your `MainActivity.java`:

``` java
import com.rollbar.android.Rollbar

public class MainActivity extends AppCompatActivity {

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Rollbar.init(this);
    Rollbar.instance().error(new Exception("This is a test error")); //remove this after initial testing
  }
}
```

The first time you run this code, a new item should appear in your Rollbar project.

# Docs 

For full documentation of the Java & Android SDK, see our <a href="https://docs.rollbar.com/docs/android" target="_blank" rel="noopener">Android docs</a>.
