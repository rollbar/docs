## Installation

Install the Rollbar [node.js](https://github.com/rollbar/node_rollbar) notifier using npm:

```bash
$ npm install --save rollbar
```

## Send a Message to Rollbar

```javascript
// include and initialize the rollbar library with your access token
var rollbar = require("rollbar");
rollbar.init("{{ server_access_token }}");

// record a generic message and send to rollbar
rollbar.reportMessage("Hello world!");
```

The error should appear in your Rollbar dashboard within a few seconds.

Once you've verified you have the notifier library installed, your access token works,
and you can connect to rollbar, the [node_rollbar](https://github.com/rollbar/node_rollbar)
documentation can show you how to automatically report exceptions and log message to Rollbar.
