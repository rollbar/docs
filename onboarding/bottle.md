## Installation

To send errors to Rollbar from your Python application you should use the
<a href="http://github.com/rollbar/pyrollbar" target="_blank" rel="noopener">pyrollbar</a> package. Install pyrollbar with pip:

```python
pip install rollbar
```

## Add Rollbar to Your Bottle Application

Here's a simple Bottle application that demonstrates how you import and initialize pyrollbar
and register it as an error handler.

```python
import bottle
from rollbar.contrib.bottle import RollbarBottleReporter

rbr = RollbarBottleReporter(access_token='{{ server_access_token }}', environment='production') #setup rollbar

bottle.install(rbr) #install globally

@bottle.get('/')
def raise_error():
  '''
  When navigating to /, we'll get a regular 500 page from bottle, 
  as well as have the error below listed on Rollbar.
  '''
  raise Exception('Hello, Rollbar!')

if __name__ == '__main__':
    bottle.run(host='localhost', port=8080)
```

For additional pyrollbar configuration options, see <a href="http://github.com/rollbar/pyrollbar" target="_blank" rel="noopener">Configuring pyrollbar</a>.
