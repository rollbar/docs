## Installation

Rollbar needs to be installed like any other dependency that you intend to use by including it in your deployment package ( [Instructions here](http://docs.aws.amazon.com/lambda/latest/dg/lambda-python-how-to-create-deployment-package.html))

This basically amounts to running

```
pip install rollbar
```

## Sending a message to Rollbar

The main change that is required to get Rollbar to work is to either use the `blocking` handler

```
import rollbar
rollbar.init( token='{{ server_access_token }}', environment='production', handler='blocking')
```

or to use the decorator `rollbar.lambda_function` which will ensure that any errors/messages will be transmitted to Rollbar before your function returns regardless of whether you use the `blocking` or the default `thread` handler.

```
@rollbar.lambda_function
def lambda_handler(event, context):
    rollbar.report_message('Hello from Lambda', 'info')
    return 'Hello Lambda'
```

We recommend using the decorator in all situations, but it is technically not necessary when using the `blocking` handler.
