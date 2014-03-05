# Items

These calls require a project-level access token, which should be provided in the query string. The prefix for all URLs is `https://api.rollbar.com`

<!-- Sub:[TOC] -->

## Get an item

    GET /api/1/item/:id

Requires `read` scope.


## List all items

Returns all items in the project, in pages of 20.

    GET /api/1/items/

Requires `read` scope.


### Query String Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `read`-scope project access token.
`status`|`string`|If not empty, only items with the specified status will be returned. Valid values: `'active'`, `'resolved'`
`ids`|comma-separated list of integers|If not empty, list of item IDs to return, instead of using all items in the project.
`page`|`integer`|Page number, starting from 1. 20 items are returned per page.

### Example

Get the 21st through 40th active items:

```bash
curl 'https://api.rollbar.com/api/1/items/?access_token=abcd5678&status=active&page=2'
```


## Modify an item

    PATCH /api/1/item/:id

Used to modify an item's state; currently only supports changing the status.

### Query String Parameters

The following params should be provided in the query string:

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `write`-scope project access token.

### Body Parameters

The following params must be supplied as JSON, and as the body of the request. Be sure to set the header `Content-Type: application/json`.

Name | Type | Description
-----|------|-------------
`status`|`string`|**Required.** Valid values: `'active'`, `'resolved'`

### Examples

Mark item `275123456` as resolved:

```
curl -X PATCH 'https://api.rollbar.com/api/1/item/275123456?access_token=abcd1234abcd1234' \
  --header "Content-Type: application/json" \
  --data '{"status": "resolved"}'
```


-----

Last updated: March 5, 2014
