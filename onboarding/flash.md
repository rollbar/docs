1. Download the <a href="https://github.com/rollbar/flash_rollbar/tree/master/src" target="_blank" rel="noopener">flash_rollbar</a> code or just the <a href="https://github.com/rollbar/flash_rollbar/blob/master/build/swc/Rollbar.swc" target="_blank" rel="noopener">Rollbar.swc</a> file.
2. Place the ```flash_rollbar/src``` directory in your source path or place the ```Rollbar.swc``` file in your project's library path.
3. Call ```Rollbar.init(this, accessToken, environment);``` from your top-level ```DisplayObject```.

```actionscript
package {
  import com.rollbar.notifier.RollbarNotifier;

  public class MyApp extends Sprite {
    
    public static const ROLLBAR_ACCESS_TOKEN:String = "{{ client_access_token }}";

    public function MyApp() {
      var environment:String = isDebug() ? "development" : "production";
      var person:Object = {id: getUserId(), email: getEmail(), name: getName()};  // optional
      Rollbar.init(this, ROLLBAR_ACCESS_TOKEN, environment, person);
    }
  }
}
```

```Rollbar.init()``` installed a global error handler, so you don't need to do anything else.

