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

```javascript    
    // require and initialize Rollbar
    var Rollbar = require('rollbar');
    var rollbar = new Rollbar({accessToken: "{{ server_access_token }}"});

    exports.handler = (event, context, callback) => {
      // log a message and send it to Rollbar
      rollbar.log('Hello, Lambda');
      var resp = {
        "isBase64Encoded": false,
        "statusCode": 200,
        "body": '{"hello": "lambda"}'
      };
      callback(null, resp);
    };
```

For full instructions on integrating Rollbar in your Lambda functions, see our [Rollbar.js docs](/docs/notifier/rollbar.js/#lambda).
