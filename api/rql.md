# RQL

These calls require a project-level access token with `read` scope, which should be provided in
the query string. The prefix for all URLs is `https://api.rollbar.com`.

## Create a RQL job

Creates a new RQL job if `force_refresh` is true or one for the same `query_string` does not
already exist. Returns the found or newly-created RQL job object.

    POST /api/1/rql/jobs

### POST parameters

Name | Type | Description
-----|------|-------------
`query_string`|`string`|**Required.** The RQL string to use for the job
`force_refresh`|`bool`| Force job creation, `1/true` or `0/false`. Default: `false`

Params must be supplied as JSON, and as the body of the request. Be sure to set the
header `Content-Type: application/json`.

Example cURL request:

`curl --data "query_string=select * from item_occurrence where item.counter=1&access_token=[your read access token here]" https://api.rollbar.com/api/1/rql/jobs`


### Response

The response will be a RQL Job resource, example:

```js
{
  "err" 0,
  "result": {
    "id": 123,  // job id
    "project_id": 456,
    "query_string": "show tables",
    "status": "new", // One of "new", "running", "success", "failed", "cancelled", or "timed_out"
    "job_hash": "abcdefabcdefabcdef",
    "date_created": 1446598885,
    "date_modified": 1446598885
  }
}
```


## Cancel a RQL job

Cancels the job with the given :job_id (must be a valid RQL job id for this project).

    POST /api/1/rql/job/:job_id/cancel

### Response

The response will be a RQL Job resource, example:

```js
{
  "err" 0,
  "result": {
    "id": 123,  // job id
    "project_id": 456,
    "query_string": "show tables",
    "status": "new", // One of "new", "running", "success", "failed", "cancelled", or "timed_out"
    "job_hash": "abcdefabcdefabcdef",
    "date_created": 1446598885,
    "date_modified": 1446598885
  }
}
```


## Get a RQL job

Returns the job metadata and, optionally, the current value of the job result.

    GET /api/1/rql/job/:job_id

### Query string parameters

Name | Type | Description
-----|------|-------------
`expand`|`string`|If the value is 'result', the response will contain the job result

### Response

The response will be a RQL Job resource, example:

```js
{
  "err" 0,
  "result": {
    "id": 123,  // job id
    "project_id": 456,
    "query_string": "show tables",
    "status": "new", // One of "new", "running", "success", "failed", "cancelled", or "timed_out"
    "job_hash": "abcdefabcdefabcdef",
    "date_created": 1446598885,
    "date_modified": 1446598885,
    "result": {...} // A RQL job resource if expand=result is used in query string
  }
}
```


## Get a RQL job result

Returns the job result object for the specified job_id.

    GET /api/1/rql/job/:job_id/result


### Query string parameters

Name | Type | Description
-----|------|-------------
`expand`|`string`|If the value is 'job', the response will contain the RQL job resource


### Response

The response will be a RQL job result resource, example:

```js
{
  "err" 0,
  "result": {
    "job_id": 123,  // job id
    "result": {
      "rows": [{...}],
      "selectionColumns": [...],
      "columns": [...],
      "errors": [],
      "warnings": [],
      "rowcount": 1,
      "executionTime": 123
    },
    "job": {...} // A RQL job resource if expand=job is set in the query string
  }
}

```


## List all RQL jobs

Returns a list of RQL job resources from the project. The response will be a list of RQL job
resources ordered by job id descending and paginated at 20 per page.

    GET /api/1/rql/jobs

### Response

```js
{
  "err" 0,
  "result": [
    { ... }, // RQL job resource
      ...
  ]
}
```


### Query string parameters

Name | Type | Description
-----|------|-------------
`page`|`number`|Page number starting from 1


-----
Last updated: August 27, 2017
