# Projects

These calls require an account-level access token, which should be provided in the query string.
The prefix for all URLs is `https://api.rollbar.com`


## List your projects

Lists all projects for the authenticated account.

    GET /api/1/projects

Requires `read` scope.


## Get a project

    GET /api/1/project/:id

Requires `read` scope.


## Create a project

Creates a new project in the authenticated account.

    POST /api/1/projects

Requires `write` scope.

### Parameters

Name | Type | Description
-----|------|-------------
`name`|`string`|**Required.** Name of the project. Must start with a letter; can contain letters, numbers, spaces, underscores, hyphens, periods, and commas. Max length 32 characters.

Params must be supplied as JSON, and as the body of the request. Be sure to set the
header `Content-Type: application/json`.


## Delete a project

Deletes the specified project. Be careful, there is no easy undo! If you mistakenly delete a
project, please contact [support](mailto:support@rollbar.com) immediately.

    DELETE /api/1/project/:id

Requires `write` scope.


## List project access tokens

Lists all access tokens for the specified project.

    GET /api/1/project/:id/access_tokens

Requires `read` scope.


## Update rate limits for a project access token

Updates a project access token's rate limit settings.

    PATCH /api/1/project/:id/access_token/:project_access_token

Requires `write` scope.

### Parameters

Name | Type | Description
-----|------|-------------
`rate_limit_window_count`|`integer`|**Optional.** Max number of calls the token is permitted within each window. Must be greater than -1.
`rate_limit_window_size`|`integer`|**Optional.** Window duration in seconds. Must be greater than -1.

If `rate_limit_window_size` or `rate_limit_window_count` is set to `0`, the access token will have
no rate limit. Params must be supplied as JSON, and as the body of the request. Be sure to set
the header `Content-Type: application/json`.

-----
Last updated: August 27, 2017
