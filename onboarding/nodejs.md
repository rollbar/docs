## Installation

Install the Rollbar <a href="https://github.com/rollbar/rollbar.js" target="_blank" rel="noopener">rollbar.js</a> notifier using npm:

```bash
$ npm install --save rollbar
```

## Send a Message to Rollbar

```javascript
// include and initialize the rollbar library with your access token
var Rollbar = require("rollbar");
var rollbar = new Rollbar("{{ server_access_token }}");

// record a generic message and send it to Rollbar
rollbar.log("Hello world!");
```

The message should appear in your Rollbar dashboard within a few seconds.

Once you've verified you have the notifier library installed, your access token works,
and you can connect to Rollbar, the <a href="https://github.com/rollbar/rollbar.js" target="_blank" rel="noopener">rollbar.js</a>
documentation can show you how to automatically report exceptions and log messages to Rollbar.
