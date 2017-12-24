# Filter or Ignore Errors from Bots

Rollbar provides a few ways to filter or ignore errors that happen in
requests made by bots.

### Using Custom Grouping

You can create a [Custom Grouping](https://rollbar.com/docs/custom-grouping/) rule to group all
errors from known bots into their own Item in Rollbar, separate from
your other data. Then mute that item or change its severity.

Here's an example custom grouping rule to ignore client-side JavaScript
errors that are caused by the Baidu spider:

```json
[
   {
     "condition": {
       "all": [
         {
           "eq": "browser",
            "path": "platform"
         },
         {
           "eq": "browser-js",
            "path": "framework"
        },
        {
         "eq": "Mozilla/5.0 (compatible; Baiduspider/2.0; +http://www.baidu.com/search/spider.html)",
          "path": "client.javascript.browser"
        }
      ]
    },
    "fingerprint": "Baiduspider js error",
    "title": "Baiduspider js error"
  }
]
```

We use this ourselves: these errors are still tracked in case we need
them, but they stay out of sight in day-to-day use.

### Filtering Client-Side

If you would rather ignore them completely, you can filter them out
before they are sent to the Rollbar API in the first place. For example,
for client-side JavaScript:

```js
_rollbarConfig = {
  // current config...
  checkIgnore: function(isUncaught, args, payload) {
     if (window.navigator.userAgent && window.navigator.userAgent.indexOf('Baiduspider') !== -1) {
       // ignore baidu spider
       return true;
     }
     // no other ignores
     return false;
   }
}
```

Some of our other libraries don't implement `checkIgnore` yet. Please check out the docs for your SDK to see if `checkIgnore` is implemented, and open an issue on the appropriate repo in GitHub if you'd like `checkIgnore` in an SDK that hasn't implemented it yet.
