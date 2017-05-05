## Installation with Composer (recommended)

Add `rollbar/rollbar` to your `composer.json`:

```json
{
    "require": {
        "rollbar/rollbar": "~1.0"
    }
}
```

## Manual Installation
Even if you're not using composer for your project, you still need the composer package to install rollbar-php dependencies.

1. If you don't have composer yet, follow these instructions to get the package: [install composer](https://getcomposer.org/doc/00-intro.md).
2. Clone git repository rollbar/rollbar-php into a your external libraries path: git clone https://github.com/rollbar/rollbar-php
3. Install rollbar-php dependencies: cd rollbar-php && composer install && cd ..
4. Require rollbar-php in your PHP scripts: require_once YOUR_LIBS_PATH . '/rollbar-php/vendor/autoload.php';

### Send a Test Message
Add the following code at your application's entry point:
```php
<?php
use \Rollbar\Rollbar;

// Installs global error and exception handlers
$config = array(
    // required
    'access_token' => '{{ server_access_token }}',
    // optional - environment name
    'environment' => 'production',
    // optional - path to directory your code is in. Used for linking stack traces.
    'root' => '/Users/brian/www/myapp'
);
Rollbar::init($config);

try {
    throw new \Exception('test exception');
} catch (\Exception $e) {
    Rollbar::log(Level::error(), $e);
}

// Message at level 'info'
Rollbar::log(Level::info(), 'testing info level');

// With extra data (3rd arg) and custom payload options (4th arg)
Rollbar::log(
    Level::info(),
    'testing extra data',
    array("some_key" => "some value") // key-value additional data
);

// If you want to check if logging with Rollbar was successful
$response = Rollbar::log(Level::info(), 'testing wasSuccessful()');
if (!$response->wasSuccessful()) {
    throw new \Exception('logging with Rollbar failed');
}

// Raises an E_NOTICE which will *not* be reported by the error handler
$foo = $bar;

// Will be reported by the exception handler
throw new \Exception('testing exception handler');
?>
```
Within a few seconds of loading this page, the message and errors should appear in your Rollbar dashboard.

Once you've verified you have the notifier library installed, your access token works, and you can connect to Rollbar, the [rollbar-php documentation](https://github.com/rollbar/rollbar-php) can show you how to automatically report exceptions and log messages to Rollbar.

## Note for Heroku Users:
First, add the addon:
`heroku addons:create rollbar:free`
The `access_token` and `root` config variables are automatically set, so the config should simply be:
```php
<?php
use Rollbar\Rollbar;

Rollbar::init(array(
    'environment' => 'production'
));
?>
```
