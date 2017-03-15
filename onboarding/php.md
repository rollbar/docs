## Installation

### General

Download <a href="https://raw.githubusercontent.com/rollbar/rollbar-php/v0.18.2/src/rollbar.php" target="_blank" rel="noopener">rollbar.php</a> and <a href="https://raw.githubusercontent.com/rollbar/rollbar-php/v0.18.2/src/Level.php" target="_blank" rel="noopener">Level.php</a>
and put them together somewhere you can access.

### If Using Composer

Add `rollbar/rollbar` to your `composer.json`:

```json
{
    "require": {
        "rollbar/rollbar": "~0.18.2"
    }
}
```

### Upcoming Release

If you'd like to run the next release of rollbar-php, you can use it via composer by adding the following to
your `composer.json`

```json
{
    "require": {
        "rollbar/rollbar": "~1.0.0-beta"
    }
}
```

## Send a Message to Rollbar

Add the following code to one of your PHP pages:

```php
<?php
// installs global error and exception handlers
Rollbar::init(array('access_token' => '{{ server_access_token }}'));

// Message at level 'info'
Rollbar::report_message('testing 123', 'info');

// Catch an exception and send it to Rollbar
try {
    throw new Exception('test exception');
} catch (Exception $e) {
    Rollbar::report_exception($e);
}

// Will also be reported by the exception handler
throw new Exception('test 2');
?>
```

Within a few seconds of loading this page, the message and errors should appear in your Rollbar dashboard.

Once you've verified you have the notifier library installed, your access token works,
and you can connect to rollbar, the <a href="https://github.com/rollbar/rollbar-php" target="_blank" rel="noopener">rollbar-php</a>
documentation can show you how to automatically report exceptions and log message to Rollbar.
