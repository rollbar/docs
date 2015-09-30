## Installation

To send errors to Rollbar from your Ruby application you should use
[rollbar-gem](http://github.com/rollbar/rollbar-gem) notifier library.

If you're using bundler, add

```ruby
gem 'rollbar', '~> 1.5.3'
```

and run

```sh
bundle install
```

otherwise you can simply

```sh
gem install rollbar
```

## Add Rollbar to Your Rack Application

Initialize Rollbar with your access token somewhere during startup:

```ruby
Rollbar.configure do |config|
  config.access_token = '{{ server_access_token }}'
  # other configuration settings
  # ...
end
```

<!-- RemoveNextIfProject -->
Be sure to replace ```{{ server_access_token }}``` with your project's ```post_server_item``` access token, which you can find in the Rollbar.com interface.

This monkey patches `Rack::Builder` to work with Rollbar automatically.

For more control, disable the monkey patch:

```ruby
Rollbar.configure do |config|
  config.disable_monkey_patch = true
  # other configuration settings
  # ...
end
```

Then mount the middleware in your app, like:

```ruby
class MyApp < Sinatra::Base
  use Rollbar::Middleware::Sinatra
  # other middleware/etc
  # ...
end
```

## Test your installation

To confirm that your application is properly configured, run:

```bash
$ rake rollbar:test
```

This will raise an exception within a test request; if it works, you'll see a stacktrace in the console, and the exception will appear in the Rollbar dashboard.


