Rollbar has an API endpoint that is wire-compatible with the Airbrake Notices API v2.2. 
If you are currently an Airbrake user, this may be your easiest way to get started.

To use, configure your library to use the host api.rollbar.com (if it is configured with a host) or the URL
https://api.rollbar.com/notifier_api/v2/notices (if it is configured with a URL).

For example, if using the Airbrake Rails gem, put the following in config/initializers/airbrake.rb:

```ruby
Airbrake.configure do |config|
  config.api_key = '{{ server_access_token }}'
  config.host = 'api.rollbar.com'
  config.secure = true
end
```

Not all Rollbar features are available through this endpoint, so when possible we recommend using a Rollbar-specific library instead.
