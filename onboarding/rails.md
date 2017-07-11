## Install the gem

Add to your Gemfile:

```ruby
gem 'rollbar'
```

Then run:

```shell
bundle install
```

If you don't use bundler:

```
gem install rollbar
```


## Add Rollbar to Your Rails Application

Run the following command from your Rails root:

```bash
rails generate rollbar {{ server_access_token }}
```

That will create the file ```config/initializers/rollbar.rb```, which initializes Rollbar and holds your access token and other configuration values.

## Test Your Rollbar Configuration

To confirm that your application is properly configured, run:

```bash
$ rake rollbar:test
```

This will raise an exception within a test request; if it works, you'll see a stacktrace in the console, and the exception will appear in the Rollbar dashboard.

## Advanced Options

If you want to store your access token outside of your repo, run the same command without arguments and create an environment variable ```ROLLBAR_ACCESS_TOKEN``` that holds your server-side access token:

```bash
$ rails generate rollbar
$ export ROLLBAR_ACCESS_TOKEN={{ server_access_token }}
```

### For Heroku users

If you're on Heroku, you can store the access token in your Heroku config:

```bash
$ heroku config:add ROLLBAR_ACCESS_TOKEN={{ server_access_token }}
```
