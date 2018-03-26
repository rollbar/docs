---
title: API Reference - Deploys
---

# Deploys

These calls require a project-level access token, which should be provided in the query string.
The prefix for all URLs is `https://api.rollbar.com`.

---

## Record (create) a deploy

    POST /api/1/deploy/

Requires `post_server_item` scope.

### Form Data Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `post_server_item`-scope project access token.
`environment`|`string`|**Required.** Name of the environment being deployed. (String up to 255 chars)
`revision`|`string`|**Required.** String identifying the revision being deployed, such as a Git SHA. (String up to 255 chars). This param can also be provided under the name `head_long`.
`rollbar_username`|`string`|Rollbar username of the user who deployed.
`local_username`|`string`|Username (on your system) who deployed. (String up to 255 chars)
`comment`|`string`|Additional text data to record with this deploy. (String up to 64kb)

### Examples

See our example integrations for tracking deploys from
[Bash](https://rollbar.com/docs/deploys/bash/),
[Capistrano](https://rollbar.com/docs/deploys/capistrano/),
[Engine Yard](https://rollbar.com/docs/deploys/engineyard/),
[Fabric](https://rollbar.com/docs/deploys/fabric/),
[Heroku](https://rollbar.com/docs/deploys/heroku/), and
[MSBuild](https://rollbar.com/docs/deploys/msbuild/).

Record a deploy of the "production" environment, revision "aaaafff", rollbar user "brianr", with
comment "just a test":

```bash
curl 'https://api.rollbar.com/api/1/deploy/' -F access_token=abcdef1234 -F environment=production -F revision=aaaafff -F rollbar_username=brianr -F comment="just a test"
```


---

## Get a deploy by ID

    GET /api/1/deploy/:id

Requires `read` scope.

`:id` must be an ID for a deploy in the project. These IDs are returned as the `id` field in other
API calls, and can be found in the Rollbar UI on URLs like "https://rollbar.com/deploy/12345/"
(12345 is the Deploy ID).


---

## List all deploys

Returns all deploys in the project, most recent first, in pages of 20.

    GET /api/1/deploys/

Requires `read` scope.


### Query String Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `read`-scope project access token.
`page`|`integer`|Page number, starting from 1. 20 deploys are returned per page.

### Examples

Get the 20 most recent deploys:

```bash
curl 'https://api.rollbar.com/api/1/deploys/?access_token=abcd5678'
```

Get the 21st through 40th most recent deploys:

```bash
curl 'https://api.rollbar.com/api/1/deploys/?access_token=abcd5678&page=2'
```


-----
Last updated: August 27, 2017
