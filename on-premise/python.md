# Python for On-Premises Installations

Using the python client with your on-premises installation is mostly the
same as using it with the regular rollbar.com service, with a few minor
tweaks.

First, you'll ned to supply the endpoint for your internal installation
so the code knows where to send the rollbar errors and messages:

`endpoint = https://<internal fqdn>/api/1/`

Then, if you're using the default, self-generated SSL certificates,
you'll need to tell python to ignore the fact that it's not really a
valid certificate:

`verify_https = False`

You'll need to put these additional parameters into the configuration
you use for the particular python environment you're running in,
eg. Django, Pyramid, Flask, etc...  Here's an example of the changes
needed for a couple of common cases.  You can adapt this to your
particular environment.

## generic python client

The new settings will go into your init call:

```py
rollbar.init('POST_SERVER_ITEM_ACCESS_TOKEN',
             'ENVIRONMENT',
             endpoint='https://<internal fqdn>/api/1/',
             verify_https=False)
```

## django

The new settings will go into `settings.py`:

```py
ROLLBAR = {
    'access_token': 'POST_SERVER_ITEM_ACCESS_TOKEN',
    'environment': 'development' if DEBUG else 'production',
    'branch': 'master',
    'root': '/absolute/path/to/code/root',
    'endpoint': 'https://<internal fqdn>/api/1/',
    'verify_https': False
}
```
