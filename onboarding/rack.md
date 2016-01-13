## Install the gem

Add to your Gemfile:

```ruby
gem 'rollbar', '~> 2.7.1'
```

Then run:

```shell
bundle install
```

If you don't use bundler:

```
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
