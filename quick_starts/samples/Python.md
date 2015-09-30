## Install the library

Using pip:

```python
pip install rollbar
```

## Import and configure the library

```python
import rollbar

rollbar.init('POST_SERVER_ITEM_ACCESS_TOKEN', 'production')  # access_token, environment
```

Be sure to replace `POST_SERVER_ITEM_ACCESS_TOKEN` with your project's `post_server_item` access token.

This is all what you need to start sending your Python errors to Rollbar automatically.

## Test it

In order to test the library you can send a message report to Rollbar:

```python
rollbar.report_message('this is a test')
```

Open your project's item list page and you should be able to see a new error with the given message.

## Send error reports

You can send a error report for your rescued exceptions using `rollbar.report_exc_info()`:

```python
try:
   # Some code that crashes
 except:
   rollbar.report_exc_info()
```