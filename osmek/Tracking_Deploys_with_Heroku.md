<span class="date">05/14/14 at 07:19 PM</span>

Use the free Deploy Hook addon from Heroku. Run this command to add it
to your Heroku app:

``` {data-language="bash"}
heroku addons:create deployhooks:http --url="https://api.rollbar.com/api/1/deploy/?access_token=POST_SERVER_ITEM_ACCESS_TOKEN&environment=production"
```

Note that this includes your Rollbar project access token and the
environment name "production".

If you already have an HTTP deploy hook set up, you'll need to remove it
first:

``` {data-language="bash"}
heroku addons:destroy deployhooks:http
```
