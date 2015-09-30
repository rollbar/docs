---
access_token: 'POST_SERVER_ACCESS_TOKEN'
---
## Add Rollbar to Your Django Application

In your ``settings.py``, add ``'rollbar.contrib.django.middleware.RollbarNotifierMiddleware'`` as the last item in ``MIDDLEWARE_CLASSES``:

```python
MIDDLEWARE_CLASSES = (
    # ... other middleware classes ...
    'rollbar.contrib.django.middleware.RollbarNotifierMiddleware',
)
```

Add these configuration variables in ``settings.py``:

```python
ROLLBAR = {
    'access_token': '{{ access_token }}',
    'environment': 'development' if DEBUG else 'production',
    'branch': 'master',
    'root': '/absolute/path/to/code/root',
}
```

For additional pyrollbar configuration options, see [Configuring pyrollbar](https://github.com/rollbar/pyrollbar).
