## Installation
Install using composer:

### Laravel 5.6 and later:
```
composer require rollbar/rollbar-laravel
```

### Laravel 5.5 and earlier
```
composer require rollbar/rollbar-laravel 2.*
```

## Configuration
Add Project Access Token to `.env`:
```
ROLLBAR_TOKEN="{{ server_access_token }}"
```

Add the service provider to the `'providers'` array in `config/app.php`:

```php
<?php
Rollbar\Laravel\RollbarServiceProvider::class,
```

### Laravel 5.6 and later:
In `config/logging.php`, add `rollbar` logging channel by adding the following under `channel` key:

```php
<?php
        'rollbar' => [
            'driver' => 'monolog',
            'handler' => \Rollbar\Laravel\MonologHandler::class,
            'access_token' => env('ROLLBAR_TOKEN'),
            'level' => 'error',
        ]
```

## Send a test message
Add the following code to send a test message and confirm that Rollbar is properly configured:

```php
\Log::debug('Test debug message');
```
## Additional Setup Instructions

For full setup instructions for rollbar-laravel, see our docs:
* [Laravel 5.6 and later](https://docs.rollbar.com/docs/laravel)
* [Laravel 5.5 and earlier](https://docs.rollbar.com/docs/laravel-55)
