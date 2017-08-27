# Provisioning

Last updated: August 5, 2013

## Users

To create a new Rollbar user, call the ```provision/user``` endpoint with the following params:

username
:  Must be unique across all Rollbar usernames.

   The username must match the following regular expression, ```[a-zA-Z][a-zA-Z0-9_-]*```.

email
:  Must be unique across all Rollbar email addresses. This will be the default email address used
   for all communication, including alerts and forgotten password emails.

password
:  Passwords are never stored on our servers and are encrypted via HTTPS during transmission.

source
: Optional string used to identify where this account was provisioned from.


When a new user is provisioned an account and starter project are also created.

### Example

```bash
curl "https://api.rollbar.com/api/1/provision/user/" -d"username=test" -d"email=test@rollbar.com" -d"password=PA$$w0RD"
```

Response

```javascript
{
  "err": 0,
  "result": {
    "access_tokens": {
      "ACCESS_TOKEN_1": [
        "write"
      ],
      "ACCESS_TOKEN_2": [
        "read"
      ],
      "ACCESS_TOKEN_3": [
        "post_server_item"
      ],
      "ACCESS_TOKEN_4": [
        "post_client_item"
      ]
    },
    "project_id": 12345,
    "user_id": 928192,
    "account_id": 28392,
    "project_url": "https://rollbar.com/project/12345/"
  }
```

-----
Last updated: August 27, 2017
