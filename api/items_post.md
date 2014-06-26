_**Note:**  This documentation is provided for authors of custom integration libraries. If your application is built on one of our supported platforms, you can use a pre-built library instead of rolling your own._

### Overview

Rollbar receives Occurrences (exceptions and messages) via a RESTful JSON API. Clients send JSON data via an HTTP POST to `https://api.rollbar.com/api/1/item/`

We strongly recommend using HTTPS, but HTTP is also supported. For HTTP, use `http://api.rollbar.com/api/1/item/`

POSTed JSON data is accepted either as the body of the request, or form-encoded as the value of the `payload` parameter (which should be the only parameter).

All responses (including error responses) are returned as JSON.

### Simple Example

Here is a bare-bones request to report a message using Python. Note that the `access_token` is part of the JSON payload, and that the encoded JSON payload is sent as the request body.

```python
import json, requests

payload = {
  "access_token": "POST_SERVER_ITEM_ACCESS_TOKEN",
  "data": {
    "environment": "production",
    "body": {
      "message": {
        "body": "Hello, world!"
      }
    }
  }
}

json_encoded_payload = json.dumps(payload)
requests.post('https://api.rollbar.com/api/1/item/', data=json_encoded_payload)
```

If your library does not allow you to specify the raw POST body, you can send it form-encoded as the value of the <code>payload</code> parameter. For example, using Python:

```python
requests.post('https://api.rollbar.com/api/1/item/', data={'payload': json_encoded_payload})
```

### Data Format

The example JSON payload below describes all the required and optional params that Rollbar understands. The meaning of each key is explained in the comments.

```javascript
{
  // Required: access_token
  // An access token with scope "post_server_item" or "post_client_item".
  // A post_client_item token must be used if the "platform" is "browser", "flash", "android", or "ios"
  // A post_server_item token should be used for other platforms.
  "access_token": "aaaabbbbccccddddeeeeffff00001111",

  // Required: data
  "data": {

    // Required: environment
    // The name of the environment in which this occurrence was seen.
    // A string up to 255 characters. For best results, use "production" or "prod" for your
    // production environment.
    // You don't need to configure anything in the Rollbar UI for new environment names; 
    // we'll detect them automatically.
    "environment": "production",

    // Required: body
    // The main data being sent. It can either be a message or an exception.
    "body": {

      // Required: "trace", "trace_chain", or "message" (exactly one)
      // If this payload is a single exception, use "trace"
      // If a chain of exceptions (for languages that support inner exceptions), use "trace_chain"
      // If a message with no stack trace, use "message"

      // Option 1: "trace"
      "trace": {

        // Required: frames
        // A list of stack frames, ordered such that the most recent call is last in the list.
        "frames": [
          // Each frame is an object.
          {
            // Required: filename
            // The filename including its full path.
            "filename": "/Users/brian/www/mox/mox/views/project.py",

            // Optional: lineno
            // The line number as an integer
            "lineno": 26,
            
            // Optional: colno
            // The column number as an integer
            "colno": 8,

            // Optional: method
            // The method or function name
            "method": "index",

            // Optional: code
            // The line of code
            "code": "_save_last_project(request, project_id, force=True)",

            // Optional: context
            // Additional code before and after the "code" line
            "context": {
              // Optional: pre
              // List of lines of code before the "code" line
              "pre": [
                "project = request.context",
                "project_id = project.id"
              ],

              // Optional: post
              // List of lines of code after the "code" line
              "post": []
            },

            // Optional: args
            // List of values of positional arguments to the method/function call
            // NOTE: as this can contain sensitive data, you may want to scrub the values
            "args": ["<Request object>", 25],

            // Optional: kwargs
            // Object of keyword arguments (name => value) to the method/function call
            // NOTE: as this can contain sensitive data, you may want to scrub the values
            "kwargs": {
              "force": true
            }
          },
          {
            "filename": "/Users/brian/www/mox/mox/views/project.py",
            "lineno": 497,
            "method": "_save_last_project",
            "code": "user = foo"
          }
        ],

        // Required: exception
        // An object describing the exception instance.
        "exception": {
          // Required: class
          // The exception class name.
          "class": "NameError",
          
          // Optional: message
          // The exception message, as a string
          "message": "global name 'foo' is not defined"
        }
      
      },

      // Option 2: "trace_chain"
      // Used for exceptions with inner exceptions or causes
      "trace_chain": [
        // Each element in the list should be a "trace" object, as shown above
        // Must contain at least one element.
      ],

      // Option 3: "message"
      // Only one of "trace", "trace_chain", or "message" should be present.
      // Presence of a "message" key means that this payload is a log message.
      "message": {
        
        // Required: body
        // The primary message text, as a string
        "body": "Request over threshold of 10 seconds",

        // Can also contain any arbitrary keys of metadata. Their values can be any valid JSON.
        // For example:

        "route": "home#index",
        "time_elapsed": 15.23

      }
    
    },

    // Optional: level
    // The severity level. One of: "critical", "error", "warning", "info", "debug"
    // Defaults to "error" for exceptions and "info" for messages.
    // The level of the *first* occurrence of an item is used as the item's level.
    "level": "error",

    // Optional: timestamp
    // When this occurred, as a unix timestamp.
    "timestamp": 1369188822,

    // Optional: platform
    // The platform on which this occurred. Meaningful platform names:
    // "browser", "flash", "android", "ios", "heroku", "google-app-engine"
    // If this is a client-side event, be sure to specify the platform and use a post_client_item access token.
    "platform": "linux",

    // Optional: language
    // The name of the language your code is written in.
    "language": "python",

    // Optional: framework
    // The name of the framework your code uses
    "framework": "pyramid",

    // Optional: context
    // An identifier for which part of your application this event came from.
    // Items can be searched by context (prefix search)
    // For example, in a Rails app, this could be `controller#action`. 
    // In a single-page javascript app, it could be the name of the current screen or route.
    "context": "project#index",

    // Optional: request
    // Data about the request this event occurred in.
    "request": {
      // Can contain any arbitrary keys. Rollbar understands the following:

      // url: full URL where this event occurred
      "url": "https://rollbar.com/project/1",

      // method: the request method
      "method": "GET",

      // headers: object containing the request headers.
      "headers": {
        // Header names should be formatted like they are in HTTP.
        "Accept": "text/html",
        "Referer": "https://rollbar.com/"
      },

      // params: any routing parameters (i.e. for use with Rails Routes)
      "params": {
        "controller": "project",
        "action": "index"
      },

      // GET: query string params
      "GET": {},

      // query_string: the raw query string
      "query_string": "",

      // POST: POST params
      "POST": {},

      // body: the raw POST body
      "body": "",

      // user_ip: the user's IP address as a string.
      // Can also be the special value "$remote_ip", which will be replaced with the source IP of the API request. 
      "user_ip": "100.51.43.14"

    },

    // Optional: person
    // The user affected by this event. Will be indexed.
    "person": {
      // Required: id
      // A string up to 40 characters identifying this user in your system.
      "id": "12345",

      // Optional: username
      // A string up to 255 characters
      "username": "brianr",

      // Optional: email
      // A string up to 255 characters
      "email": "brian@rollbar.com"
    },

    // Optional: server
    // Data about the server related to this event.
    "server": {
      // Can contain any arbitrary keys. Rollbar understands the following:

      // host: The server hostname. Will be indexed.
      "host": "web4",

      // root: Path to the application code root, not including the final slash.
      // Used to collapse non-project code when displaying tracebacks.
      "root": "/Users/brian/www/mox",

      // branch: Name of the checked-out source control branch. Defaults to "master"
      "branch": "master",

      // sha: Git SHA of the running code revision. Use the full sha.
      "sha": "b6437f45b7bbbb15f5eddc2eace4c71a8625da8c"
    },

    // Optional: client
    // Data about the client device this event occurred on.
    // As there can be multiple client environments for a given event (i.e. Flash running inside
    // an HTML page), data should be namespaced by platform.
    "client": {
      // Can contain any arbitrary keys. Rollbar understands the following:

      "javascript": {

        // Optional: browser user agent string
        "browser": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_3)"

      }
    },

    // Optional: custom
    // Any arbitrary metadata you want to send. "custom" itself should be an object.
    "custom": {},

    // Optional: fingerprint
    // A string controlling how this occurrence should be grouped. Occurrences with the same
    // fingerprint are grouped together. See the "Grouping" guide for more information.
    // Should be a string up to 40 characters long; if longer than 40 characters, we'll use its SHA1 hash.
    // If omitted, we'll determine this on the backend.
    "fingerprint": "50a5ef9dbcf9d0e0af2d4e25338da0d430f20e52",

    // Optional: title
    // A string that will be used as the title of the Item occurrences will be grouped into.
    // Max length 255 characters.
    // If omitted, we'll determine this on the backend.
    "title": "NameError when setting last project in views/project.py",

    // Optional: notifier
    // Describes the library used to send this event.
    "notifier": {
      // Optional: name
      // Name of the library
      "name": "pyrollbar",

      // Optional: version
      // Library version string
      "version": "0.5.5"
    }

  }
}
```

Note that you can send us whatever data you want and we'll store it. Max paylaod size is 128kb. For best results, put custom data in "request", "server", "client", "person", or "custom".

### Error Responses

The Items API can return the following status codes:

<dl class="dl-horizontal">
  <dt>200</dt>
    <dd><strong>Success.</strong> The item was accepted for processing.</dd>
  <dt>400</dt>
    <dd><strong>Bad request.</strong> No JSON payload was found, or it could not be decoded.</dd>
  <dt>401</dt>
    <dd><strong>Unauthorized.</strong> No access token was found in the request.</dd>
  <dt>403</dt>
    <dd><strong>Access denied.</strong> Check that your <code>access_token</code> is valid, enabled, and has the correct scope. The response will contain a `message` key explaining the problem.</dd>
  <dt>413</dt>
    <dd><strong>Request Too Large.</strong> Max payload size is 128kb. Try removing or truncating unnecessary large data included in the payload, like whole binary files or long strings.</dd>
  <dt>422<dt>
    <dd><strong>Unprocessable payload.</strong> A syntactically valid JSON payload was found, but it had one or more semantic errors. The response will contain a "message" key describing the errors.</dd>
  <dt>429</dt>
    <dd><strong>Too Many Requests</strong> - Request dropped because the rate limit has been reached for this access token, or the account is on the Free plan and the plan limit has been reached.</dd>
  <dt>500</dt>
    <dd><strong>Internal server error.</strong> There was an error on Rollbar's end.</dd>
</dl>

If you encounter any other errors, or don't understand an error you see, please [contact support](/support).
