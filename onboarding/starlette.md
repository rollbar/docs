This is a quick starter guide for Starlette applications.

You can check further instructions for Starlette integration in our <a href="https://docs.rollbar.com/docs/python" target="_blank" rel="noopener">Complete Python Documentation</a>.
Starlette integration examples are also available in our <a href="https://github.com/rollbar/pyrollbar/tree/master/rollbar/examples/starlette" target="_blank" rel="noopener">GitHub repository</a>.

## Installation

Use the <a href="https://github.com/rollbar/pyrollbar" target="_blank" rel="noopener">pyrollbar</a> SDK for sending events to Rollbar from your Starlette application.

Install pyrollbar with pip:

```shell script
pip install rollbar
```

## Test your Integration

```python
import rollbar
from rollbar.contrib.starlette import ReporterMiddleware as RollbarMiddleware
from starlette.applications import Starlette

# Initialize Rollbar SDK with your server-side access token
rollbar.init('{{ server_access_token }}')

# Integrate Rollbar with Starlette application
app = Starlette()
app.add_middleware(RollbarMiddleware)  # should be added as the first middleware

# Add an /error endpoint to cause an uncaught exception
async def localfunc(arg1, arg2, arg3):
    # Both local variables and function arguments will be sent to Rollbar
    # and available in the UI
    localvar = 'local variable'
    cause_error_with_local_variables


@app.route('/error')
async def error(request):
    await localfunc('func_arg1', 'func_arg2', 1)
```

Save the example as a `main.py` file and run it via ASGI-compliant server (e.g. Uvicorn, Hypercorn, Daphne).
You may need to install a server first.

```shell script
pip install uvicorn

uvicorn main:app
```

Open `http://localhost:8000/error` in your web browser.

A few seconds after you execute this code, an exception should appear on your project's "Items" page.
This item will include the basic exception information and a stack trace, along with the values of
local variables and the arguments passed to each function at each frame in the stack trace.

For more advanced configuration options, visit our <a href="https://docs.rollbar.com/docs/python#configuration-reference" target="_blank" rel="noopener">Complete Configuration reference</a>.
