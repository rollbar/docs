---
title: API Reference - Users
---

# Users

These calls require an account-level access token, which should be provided in the query string.
The prefix for all URLs is `https://api.rollbar.com`


## List all users

Lists all users who a member of the current account.

    GET /api/1/users

Requires `read` scope.    

Example response:

```json
{
  "err": 0,
  "result": {
    "users": [
      {
        "username": "brianr",
        "id": 1,
        "email": "brian@rollbar.com"
      },
      {
        "username": "coryvirok",
        "id": 2,
        "email": "cory@rollbar.com"
      }
    ]
  }
}
```


## Get a user

    GET /api/1/user/:id

Requires `read` scope.

Returns basic information about the user, as relevant to the account your access token is for.
This is the same information available on the "Members" page in the Rollbar UI.

Example response:

```json
{
  "err": 0,
  "result": {
      "id": 14,
      "username": "brian",
      "email": "brian@rollbar.com",
      "email_enabled": 1
  }
}
```

Note that `id` is immutable, but all other fields are mutable.


## List user's teams

Lists all teams in the current account that the specified user is a memebr of.

    GET /api/1/user/:id/teams

Requires `read` scope.

Example response:

```json
{
  "err": 0,
  "result": {
    "teams": [
      {
        "access_level": "owner",
        "id": 36,
        "name": "Owners",
        "account_id": 61
      },
      {
        "access_level": "standard",
        "id": 574,
        "name": "Developers",
        "account_id": 61
      }
    ]
  }
}
```


## List user's projects

Lists all projects in the current account that the specified user has access to.

    GET /api/1/user/:id/projects

Requires `read` scope.

Example response:

```json
{
  "err": 0,
  "result": {
    "projects": [
      {
        "status": 1,
        "slug": "mox",
        "id": 1,
        "account_id": 61
      },
      {
        "status": 1,
        "slug": "moxrts",
        "id": 25,
        "account_id": 61
      }
    ]
  }
}
```

-----
Last updated: August 27, 2017
