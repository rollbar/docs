This is a quick starter guide for basic Python applications.
You can check further instructions for supported Python frameworks in our <a href="https://docs.rollbar.com/docs/python" target="_blank" rel="noopener">Complete Python Documentation</a>.

## Installation

Use the <a href="https://github.com/rollbar/pyrollbar" target="_blank" rel="noopener">pyrollbar</a> SDK for sending events to Rollbar from your Python application.

Install pyrollbar with pip:

```shell script
pip install rollbar
```

## Send a Message

You'll need your project's server-side access token to initialize the pyrollbar SDK. Sending
a message to the Rollbar server is as simple as:

```python
import rollbar

rollbar.init('{{ server_access_token }}')
rollbar.report_message('Rollbar is configured correctly')
```

A few seconds after you execute this code, the message should appear on your project's "Items" page.

## Report an Error

To report errors to the Rollbar server, you'll need to call a method of `rollbar` in your exception handling code.

```python
import rollbar

rollbar.init('{{ server_access_token }}')

try:
    b = a + 1
except:
    rollbar.report_exc_info()

```
A few seconds after you execute this code, an exception should appear on your project's "Items" page.
This item will include the basic exception information and a stack trace, along with the values of
local variables and the arguments passed to each function at each frame in the stack trace.
