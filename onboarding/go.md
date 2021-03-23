<div class="alert alert-info">
	Rollbar's Go SDK is currently a <code>alpha</code> release.  For details, please see the <a href="https://github.com/rollbar/rollbar-go/blob/master/README.md">Readme</a>.<br>
	To report issues, make suggestions, or ask questions, please <a href="https://github.com/rollbar/rollbar-go/issues/new">create an issue in Github</a>.
</div>

## Installation

To send errors to Rollbar from your Go application, you should use our <a href="https://github.com/rollbar/rollbar-go" target="_blank" rel="noopener">rollbar-go</a> SDK.


You'll need your project's server-side access token to initialize the Go SDK. Sending
a message or an error to the Rollbar server is as simple as:

```go
package main

import (
  "errors"

  "github.com/rollbar/rollbar-go"
)

func main() {
  rollbar.SetToken("{{ server_access_token }}")
  rollbar.SetEnvironment("production")                 // defaults to "development"
  rollbar.SetCodeVersion("v2")                         // optional Git hash/branch/tag (required for GitHub integration)
  rollbar.SetServerHost("web.1")                       // optional override; defaults to hostname
  rollbar.SetServerRoot("github.com/heroku/myproject") // path of project (required for GitHub integration and non-project stacktrace collapsing)

  err := DoSomething()
  if err != nil {
    rollbar.Critical(err)
  }

  rollbar.Info("Message body goes here")

  rollbar.Wait()
}

func DoSomething() error {
  return errors.New("new error")
}

```

A few seconds after you execute this code, the item should appear on your project's "Items" page.
