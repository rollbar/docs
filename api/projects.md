# Projects

These calls require an account-level access token, which should be provided in the query string. The prefix for all URLs is `https://api.rollbar.com`

<!-- Sub:[TOC] -->

---

## Get a project

    GET /api/1/project/:id


## List project access tokens

    GET /api/1/project/:id/access_tokens


## List your projects

Lists projects for the authenticated account.

    GET /api/1/projects


## Create a project

Creates a new project in the authenticated account.

    POST /api/1/projects

### Parameters

Name | Type | Description
-----|------|-------------
`name`|`string`|**Required.** Name of the project. Must start with a letter; can contain letters, numbers, spaces, underscores, hyphens, periods, and commas. Max length 32 characters.

Params must be supplied as JSON, and as the body of the request. Be sure to set the header `Content-Type: application/json`.


## Delete a project

Deletes the specified project. Be careful, there is no easy undo! If you mistakenly delete a project, please contact [support](support@rollbar.com) immediately.

    DELETE /api/1/project/:id

-----

Last updated: November 26, 2013
