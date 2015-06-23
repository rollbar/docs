## Configure the library

Inside your `<head>` tag of your pages, before any other `<script>` tag paste this:

```javascript
<script>
var _rollbarConfig = {
    accessToken: "POST_CLIENT_ITEM_ACCESS_TOKEN",
    captureUncaught: true, // This will enable automatically uncaught errors reporting
    payload: {
        environment: "production"
    }
};
</script>
```

Be sure to replace `POST_CLIENT_ITEM_ACCESS_TOKEN` with your project's `post_client_item` access token.

## Add the script tag

After the `_rollbarConfig` definition, add the next line:

```javascript
<script src="https://d37gvrvc0wt4s1.cloudfront.net/js/v1.3/rollbar.umd.nojson.min.js"></script>
```

This is all what you need to start sending Javascript errors to Rollbar.

# Test it

Refresh your webpage, open a console in the inspector and write:

```javascript
var error = new Error("this is a test");
Rollbar.error(error);
```

Open your project's item list page and you should be able to see a new error.

## Send error reports manually

You can catch your Javascript errors and report them to Rollbar manually:

```javascript
try {
  // Some code that crashes
} catch (e) {
  Rollbar.error(e);
}
```