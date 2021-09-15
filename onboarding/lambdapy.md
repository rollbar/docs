## Installation

Rollbar needs to be installed like any other dependency that you intend to use by including it in your deployment package ( [Instructions here](http://docs.aws.amazon.com/lambda/latest/dg/lambda-python-how-to-create-deployment-package.html))

This basically amounts to running

```
pip install rollbar
```

## Sending a test message to Rollbar

Add the following to import and initialize Rollbar:

```
import rollbar
rollbar.init('{{ server_access_token }}', environment='production')
```

Use the decorator `rollbar.lambda_function` which will ensure that any errors/messages will be transmitted to Rollbar before your function returns:

```
@rollbar.lambda_function
def lambda_handler(event, context):
    rollbar.report_message('Hello from Lambda', 'info')
    return 'Hello Lambda'
```

For further instructions on using pyrollbar in AWS Lambda, see our [pyrollbar docs]().
