---
access_token: 'POST_SERVER_ACCESS_TOKEN'
---
## Installation

To send errors to Rollbar from your Python application you should use 
[pyrollbar](http://github.com/rollbar/pyrollbar) notifier library. Install pyrollbar with pip:

```python
pip install rollbar
```

## Send a Message

You'll need your project's server-side access token to initialize the Rollbar notifier. Sending
a message to Rollbar is as simple as:

```python
import rollbar

rollbar.init('{{ access_token }}')
rollbar.report_message('Rollbar is configured correctly')
```

A few seconds after you execute this code, the message should appear on your project's "Items" page.

## Report an Error

To report errors to Rollbar, you'll need to call the Rollbar notifier in your exception handling code.

```python
import rollbar

rollbar.init('{{ access_token }}')

try:
    b = a + 1
except:
    rollbar.report_exc_info()

```
A few seconds after you execute this code, an exception should appear on your project's "Items" page.
This item will include the basic exception information and a stack trace, along with the values of
local variables and the arguments passed to each function at each frame in the stack trace.
