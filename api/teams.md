# Teams

In Rollbar, users are allowed to access projects if they are part of a team that can access that
project. Teams belong to accounts, and can be associated (many-to-many) with Projects and Users.

These calls require an account-level access token, which should be provided in the query string.
The prefix for all URLs is `https://api.rollbar.com`


## Get a team

    GET /api/1/team/:id

Requires `read` scope.


## List your teams

Lists teams for the authenticated account.

    GET /api/1/teams

Requires `read` scope.

Returns up to 20 results. Add `&page=2` to go to the next page.



## Create a team

Creates a new team in the authenticated account.

    POST /api/1/teams

Requires `write` scope.

### Parameters

Name | Type | Description
-----|------|-------------
`name`|`string`|**Required.** Name of the team. Max length 32 characters.
`access_level`|`string`|**Required.** Can be either `standard`, `light`, or `view`.

Params must be supplied as JSON, and as the body of the request. Be sure to set the
header `Content-Type: application/json`.


## Delete a team

Deletes the specified team. Be careful, there is no undo!

    DELETE /api/1/team/:id

Requires `write` scope.

Note: the Owners team (which has access level `owner`) is special and cannot be deleted.


## Check if a project is in a team

    GET /api/1/team/:team_id/project/:project_id

Requires `read` scope.

## List projects in a team

    GET /api/1/team/:team_id/projects

Requires `read` scope.

Returns up to 20 results. Add `&page=2` to go to the next page.


## Add a project to a team

    PUT /api/1/team/:team_id/project/:project_id

Requires `write` scope.


## Remove a project from a team

    DELETE /api/1/team/:team_id/project/:project_id

Requires `write` scope.


## Check team membership

    GET /api/1/team/:team_id/user/:user_id

Requires `read` scope.


## List team members

    GET /api/1/team/:team_id/users

Requires `read` scope.

Returns up to 5000 results. Add `&page=2` to go to the next page.


## Add a user to a team

Adds an existing user (by their Rollbar User ID) to the specified team.

    PUT /api/1/team/:team_id/user/:user_id

Requires `write` scope.

## Remove a user from a team

Be careful, there is no undo!

    DELETE /api/1/team/:team_id/user/:user_id

Requires `write` scope.

-----
