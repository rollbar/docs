## Install the gem

Add the following entry to your `Gemfile`:

```ruby
gem 'rollbar'
```

Then run the command:

```shell
bundle install
```

Or, if you don't use bundler:

```
gem install rollbar
```

## Send a test message

You'll need your project's server-side access token to initialize the Rollbar gem. Sending
a message to Rollbar is as simple as:

```ruby
require 'rollbar'

Rollbar.configure do |config|
  config.access_token = '{{ server_access_token }}'
end

Rollbar.error('Hello world')
```
