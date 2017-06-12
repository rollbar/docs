## Installation with Composer (recommended)

Add `rollbar/rollbar` to your `composer.json`:

```json
{
    "require": {
        "rollbar/rollbar": "~1.1"
    }
}
```

## Send a Message to Rollbar

Add the following code to one of your PHP pages:

```php
<?php
use \Rollbar\Rollbar;

// installs global error and exception handlers
Rollbar::init(array('access_token' => '{{ server_access_token }}'));

// Message at level 'info'
Rollbar::log(Level::info(), 'testing 123');

// Catch an exception and send it to Rollbar
try {
    throw new \Exception('test exception');
} catch (\Exception $e) {
    Rollbar::log(Level::error(), $e);
}

// Will also be reported by the exception handler
throw new Exception('test 2');
?>
```

Within a few seconds of loading this page, the message and errors should appear in your Rollbar dashboard.

Once you've verified you have the notifier library installed, your access token works,
and you can connect to rollbar, the <a href="https://github.com/rollbar/rollbar-php" target="_blank" rel="noopener">rollbar-php</a> documentation can show you how to automatically report exceptions and log message to Rollbar.

## Manual Installation

If you're not using Composer, then follow the instructions in the <a href="https://github.com/rollbar/rollbar-php" target="_blank" rel="noopener">rollbar-php docs on Github</a>.

## Heroku Users

Specific instructions for Heroku users can be found in the <a href="https://github.com/rollbar/rollbar-php" target="_blank" rel="noopener">rollbar-php docs on Github</a>.



