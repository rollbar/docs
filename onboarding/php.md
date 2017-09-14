## Installation w/ Composer (recommended)

Add `rollbar/rollbar` with composer:

```bash
$ composer require rollbar/rollbar:~1.1
```

## Configuration

Add the following code to your PHP app:

```php

use \Rollbar\Rollbar;
use \Rollbar\Payload\Level;
Rollbar::init(
	array(
		'access_token' => '{{ server_access_token }}',
		'environment' => 'development'
	)
);
```
## Send a test error
Add the following to send a message and an error to Rollbar:
```php
Rollbar::log(Level::info(), 'Test info message');
throw new Exception('Test exception');
```

## Manual Installation

If you're not using Composer, then follow the instructions in the <a href="https://github.com/rollbar/rollbar-php" target="_blank" rel="noopener">rollbar-php docs on GitHub</a>.

## Heroku

Specific instructions for Heroku users can be found in the <a href="https://github.com/rollbar/rollbar-php" target="_blank" rel="noopener">rollbar-php docs on GitHub</a>.



