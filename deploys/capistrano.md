# Capistrano Deploy Integration

### Capistrano 3

Add to your `Gemfile`:

```ruby
gem 'rollbar', '~1.2.7'
```

Add to your `Capfile`:

```ruby
require 'rollbar/capistrano3'
```

Add to your `deploy.rb`:

```ruby
set :rollbar_token, 'POST_SERVER_ITEM_ACCESS_TOKEN'
set :rollbar_env, Proc.new { fetch :stage }
set :rollbar_role, Proc.new { :app }
```

NOTE: We've seen problems with Capistrano version \`3.0.x\` where the
revision reported is incorrect. Version \`3.1.0\` and higher works
correctly.

### Capistrano 2

Add to your Gemfile:

```ruby
gem 'rollbar', '~1.2.7'
```

Add to your `deploy.rb`:

```ruby
require 'rollbar/capistrano'
set :rollbar_token, 'POST_SERVER_ITEM_ACCESS_TOKEN'
```

Available options:

rollbar\_token
:   The same project access token as you used for the
    `rails generate rollbar` command; find it in
    `config/initializers/rollbar.rb`. (It's repeated here for
    performance reasons, so the rails environment doesn't have to be
    initialized.)

rollbar\_env

:   Deploy environment name

    Default: `rails_env`

For `capistrano/multistage`, try:

```ruby
set(:rollbar_env) { stage }
```
