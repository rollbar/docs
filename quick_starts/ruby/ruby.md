---
access_token: 'POST_SERVER_ACCESS_TOKEN'
---
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

## Send a Message

You'll need your project's server-side access token to initialize the Rollbar notifier. Sending
a message to Rollbar is as simple as:

```ruby
require 'rollbar'

Rollbar.configure do |config|
  config.access_token = '{{ access_token}}'
end

Rollbar.info('Rollbar is configured correctly')
```

A few seconds after you execute this code, the message should appear on your project's "Items" page.

## Report an Error

To report errors to Rollbar, you'll need to call the Rollbar notifier in your exception handling code.

```ruby
require 'rollbar'

Rollbar.configure do |config|
  config.access_token = '{{ access_token }}'
end

begin
  b = a + 1
rescue Exception => e
  Rollbar.error(e)
end
```
A few seconds after you execute this code, an exception should appear on your project's "Items" page.
This item will include the basic exception information and a stack trace, along with the values of
local variables and the arguments passed to each function at each frame in the stack trace.
## Add Rollbar to Your Ruby Application

Once you've verified that the notifier is configured correctly and can communicate with Rollbar, you'll
want to add the notifier to your existing applications. For additional configuratoin options and 
instructions for using Rollbar with specific web frameworks, see:

* [Configuring rollbar-gem](https://github.com/rollbar/rollbar-gem).
* [Using Rollbar with Rails](https://github.com/rollbar/rollbar-gem).
* [Using Rollbar with Rack](https://github.com/rollbar/rollbar-gem).
* [Tracking Capistrano Deploys]](https://github.com/rollbar/rollbar-gem).
