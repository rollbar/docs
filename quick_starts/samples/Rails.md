## Install the gem

In your `Gemfile` add this line:

```ruby
gem 'rollbar'
```

And execute `bundle install`.

## Configure Rollbar gem

Create a new Rollbar initializer in `config/initializers/rollbar.rb` the next command:

```shell
rails generate rollbar POST_SERVER_ITEM_ACCESS_TOKEN
```

Be sure to replace `POST_SERVER_ITEM_ACCESS_TOKEN` with your project's `post_server_item` access token.

This is all what you need to start sending your Rails errors to Rollbar automatically.

## Test it

Execute the next Rake task and check your project's item list at Rollbar.

```shell
rake  rollbar:test
```

## Send error reports manually

You can send manually a error report for your rescued exceptions using `Rollbar.error`:

```ruby
begin
  # Some code that crashes
rescue => e
  Rollbar.error(e)
end
```