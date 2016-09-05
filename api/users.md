# Users

These calls require an account-level access token, which should be provided in the query string.
The prefix for all URLs is `https://api.rollbar.com`


## Get a user

    GET /api/1/user/:id

Requires `read` scope.

Returns basic information about the user, as relevant to the account your access token is for.
This is the same information available on the "Members" page in the Rollbar UI.

Example response:

```json
{
  "id": 14,
  "username": "brian",
  "email": "brian@rollbar.com",
  "email_enabled": 1
}
```

Note that `id` is immutable, but all other fields are mutable.

-----

Last updated: March 24, 2014
