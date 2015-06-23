<span class="date">11/07/14 at 06:45 PM</span>

Rollbar provides a few ways to filter or ignore errors that happen in
requests made by bots.

### Using Custom Grouping

You can create a [Custom
Grouping](https://rollbar.com/docs/custom-grouping/) rule to group all
errors from known bots into their own Item in Rollbar, separate from
your other data. Then mute that item or change its severity.

Here's an example custom grouping rule to ignore client-side JavaScript
errors that are caused by the Baidu spider:

``` {data-language="json"}
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

``` {data-language="javascript"}
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

Our other libraries don't implement `checkIgnore` yet, so if you'd like
this somewhere else, please open an issue on the appropriate repo in
GitHub.
