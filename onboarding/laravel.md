## Installation
Install using composer:
```
composer require rollbar/rollbar-laravel
```

## Configuration
Add Project Access Token to `.env`:

```
ROLLBAR_TOKEN="{{ server_access_token }}"
```

Add the service provider to the `'providers'` array in `config/app.php` (this package also supports Laravel 5.5's auto-discovery, which allows you to skip this step):

```php
Rollbar\Laravel\RollbarServiceProvider::class,
```

## Send a test message
Add the following code to send a test message and confirm that Rollbar is properly configured:

```php
\Log::debug('Test debug message');
```
