## Installation

To send errors to Rollbar from your Python application you should use 
[pyrollbar](http://github.com/rollbar/pyrollbar) notifier library. Install pyrollbar with pip:

```python
pip install rollbar
```

## Add Rollbar to Your Flask Application

Here's a simple Flask app that demonstrates how you import and initialize the Rollbar
notifier end gister an exception handler.
```
from flask import Flask
app = Flask(__name__)

## Rollbar init code. You'll need the following to use Rollbar with Flask.
## This requires the 'blinker' package to be installed

import os
import rollbar
import rollbar.contrib.flask
from flask import got_request_exception


@app.before_first_request
def init_rollbar():
    """init rollbar module"""
    rollbar.init(
        # access token
        '{{ server_access_token }}',
        # environment name
        'testing',
        # server root directory, makes tracebacks prettier
        root=os.path.dirname(os.path.realpath(__file__)),
        # flask already sets up logging
        allow_logging_basic_config=False)

    # send exceptions from `app` to rollbar, using flask's signal system.
    got_request_exception.connect(rollbar.contrib.flask.report_exception, app)

## Simple flask app

@app.route('/')
def hello():
    print "in hello"
    x = None
    x[5]
    return "Hello World!"


if __name__ == '__main__':
    app.run()
```

For additional pyrollbar configuration options, see [Configuring pyrollbar](https://github.com/rollbar/pyrollbar).
