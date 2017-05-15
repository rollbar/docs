If your team is overwhelmed with a lot of noisy JavaScript errors, and you're looking for ways to reduce them, look no further. There are a few ways to reduce noisy JS errors using different Rollbar functionalities. 

## Ignore noisy errors on the client-side

[Rollbar.js](/docs/notifier/rollbar.js/) enables you to ignore errors client-side if you wish. You can filter by any value in the payload, and ensure that the error never even gets sent to the Rollbar API. To do this, use the [checkIgnore](/docs/notifier/rollbar.js/#context-1) configuration function.

```js
var _rollbarConfig = {
    ...
    checkIgnore: function(isUncaught, args, payload) {
        // Code here to determine whether or not to send the payload
        // to the Rollbar API
        // return true to ignore the payload
    }
    ...
};
```

`isUncaught` is `true` if the error bubbled up to `window.onerror`. It is false if the error came from
one of the Rollbar.js logging methods.

`args` are the args passed to the Rollbar.js logging method. If the error is uncaught and is
from an unhandled rejection, the args parameter contains the Promise object.

`payload` is the payload that will be sent to the Rollbar API. You can use anything in the
payload to conditionally filter these errors out.

To have Rollbar.js ignore the payload here, return `true` from the function. To continue processing and have the error sent to the [Rollbar API](/docs/api/), return `false`.

## Whitelist specific domains

You can configure [Rollbar.js](/docs/notifier/rollbar.js/) to only accept errors
from your own domains. We recommend this if you use a lot of third party scripts that are generating errors you have no control over, and
you only want to see errors coming from your own domains. 

```js
var _rollbarConfig = {
    ...
    hostWhiteList: ['domain1.com', 'domain2.com']
    ...
};
```

When [hostWhiteList](/docs/notifier/rollbar.js/configuration/#context) has been configured, Rollbar will
enumerate over the stack frames in each error. At
least one of the frames must contain a filename that contains at least one of the strings in this
configuration option. The items in the array are compiled into a regex that is used to compare
against the filenames. 

## Ignore certain types of messages

[Rollbar.js](/docs/notifier/rollbar.js/) allows you to ignore specific messages. This is
configured under the [ignoredMessages](/docs/notifier/rollbar.js/#ignoring-specific-exception-messages)
key. We recommend this method when you have a small sample of messages that you don't care about.

```js
var _rollbarConfig = {
    ...
    ignoredMessages: ["Can't find Clippy.bmp. The end is nigh."]
    ...
};
```

When this configuration key is set, rollbar.js looks through the values in the setting, and if any
of them match the exception message, the error will be discarded. These will be compiled into
a regex that is compared against the exception mesasge.

## Custom grouping options

We recommend using [custom grouping](/docs/custom-grouping/) when you still want the error data to be sent to
Rollbar and viewable in your dashboard for data metrics and reporting purposes, but you want to
reduce the some of the 'noise' in the [Items](/features/) list. You can set up custom grouping rules to group your
errors together in a way that makes sense for you. This is the best option to use when you still
want to see the error occurrences in your dashboard, but want full control over how they are grouped
together. See the [docs on custom grouping](/docs/custom-grouping/), as well as our in depth blog post on
[how to improve your error grouping in Rollbar](/blog/error-grouping-tutorial).

