## Installation

Run the following command to install the Rollbar library into
`node_modules` inside your code directory:

```bash
    npm install rollbar
```

This will result in a directory structure like:

```bash
    yourfunction/index.js
    yourfunction/node_modules/rollbar
    yourfunction/node_modules/...
```

## Sending a test message to Rollbar

Rollbar provides a wrapper for your Lambda function. This wrapper works with both
async and non-async function types. Simply pass your handler to `rollbar.lambdaHandler()`

### Async Lambda Handler
```javascript
// require and initialize Rollbar
const Rollbar = require('rollbar');
const rollbar = new Rollbar({accessToken: "{{ server_access_token }}"});

exports.handler = rollbar.lambdaHandler(async (event, context) => {
  // log a message and send it to Rollbar
  rollbar.log('Hello, Lambda');
  return 'ok';
}
```

### Non-Async Lambda Handler
```javascript
// require and initialize Rollbar
const Rollbar = require('rollbar');
const rollbar = new Rollbar({accessToken: "{{ server_access_token }}"});

exports.handler = rollbar.lambdaHandler((event, context, callback) => {
  // log a message and send it to Rollbar
  rollbar.log('Hello, Lambda');
  callback(null, 'ok');
});
```

For full instructions on integrating Rollbar in your Lambda functions, see our
[Rollbar.js docs](https://rollbar.com/docs/notifier/aws-lambda/).
