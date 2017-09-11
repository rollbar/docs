## Installation

Install the Rollbar <a href="https://github.com/rollbar/rollbar.js" target="_blank" rel="noopener">rollbar.js</a> notifier using npm:

```bash
$ npm install --save rollbar
```

## Configuration

Import rollbar into your app:

```
import * as Rollbar from 'rollbar';
```

Configure Rollbar to catch uncaught exceptions:

```
const rollbarConfig = {
  accessToken: '{{ client_access_token }}',
  captureUncaught: true,
  captureUnhandledRejections: true,
};
```

## Send a test error

Run the following command in your Javascript console.  Rollbar should catch the error and send it to your account:

```bash
window.onerror("TestError: Hello world", window.location.href)
```
