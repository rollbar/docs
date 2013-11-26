# Teams

In Rollbar, users are allowed to access projects if they are part of a team that can access that project. Teams belong to accounts, and can be associated (many-to-many) with Projects and Users.

<!-- Sub:[TOC] -->

----

## Get a team

    GET /api/1/team/:id


## List your teams

Lists teams for the authenticated account.

    GET /api/1/teams


## Create a team

Creates a new team in the authenticated account.

    POST /api/1/teams

### Parameters

Name | Type | Description
-----|------|-------------
`name`|`string`|**Required.** Name of the team. Max length 32 characters.
`access_level`|`string`|**Required.** Can be either `standard` or `light`.

Params must be supplied as JSON, and as the body of the request. Be sure to set the header `Content-Type: application/json`.


## Delete a team

Deletes the specified team. Be careful, there is no undo!

    DELETE /api/1/team/:id


## Check if a project is in a team

    GET /api/1/team/:team_id/project/:project_id


## List projects in a team

    GET /api/1/team/:team_id/projects


## Add a project to a team

    PUT /api/1/team/:team_id/project/:project_id


## Remove a project from a team

    DELETE /api/1/team/:team_id/project/:project_id


## Check team membership

    GET /api/1/team/:team_id/user/:user_id


## List team members

    GET /api/1/team/:team_id/users


## Remove a user from a team

Be careful, there is no undo!

    DELETE /api/1/team/:team_id/user/:user_id

-----

Last updated: November 26, 2013

