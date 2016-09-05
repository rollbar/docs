Use Engine Yard's deploy hook functionality. Simply
create deploy/after\_restart.rb in your Engine Yard app with the
following contents:

```ruby
on_app_master do
  run "curl https://api.rollbar.com/api/1/deploy/ --silent -F access_token=POST_SERVER_ITEM_ACCESS_TOKEN -F environment=#{config.environment} -F revision=#{config.revision}"
end
```
