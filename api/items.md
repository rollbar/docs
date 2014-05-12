# Items

These calls require a project-level access token, which should be provided in the query string. The prefix for all URLs is `https://api.rollbar.com`

<!-- Sub:[TOC] -->

---

## Get an item by ID

    GET /api/1/item/:id

Requires `read` scope.

`:id` must be an item ID for an item in the project. These IDs are returned as the `id` field in other API calls, and can be found in the Rollbar UI on URLs like "https://rollbar.com/item/272505123/instance/909858456/" (272505123 is the Item ID).

Note that they are NOT found in in URLs like "https://rollbar.com/project/123/item/456/" -- that is the "counter", which can be used in the following API call.


---

## Get an item by counter

    GET /api/1/item_by_counter/:counter

Requires `read` scope.

`:counter` must be an item counter for an item in the project. The counter can be found in URLs like "https://rollbar.com/project/123/item/456/" (456 is the counter).

The success response is a 301 redirect like this:

```
HTTP/1.1 301 Moved Permanently
Location: /api/1/item/272505123?access_token=abcd1234abcd1234abcd1234abcd1234

{
  "err": 0,
  "result": {
    "itemId": 272505123,
    "path": "/api/1/item/272505123",
    "uri": "/api/1/item/272505123?access_token=abcd1234abcd1234abcd1234abcd1234"
  }
}
```

Many HTTP clients will automatically follow the redirect.


---

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


---

## Modify an item

    PATCH /api/1/item/:id

Used to modify an item's state. Currently supports:

- setting the status
- when resolving, setting the "resolved in version"

### Query String Parameters

The following params should be provided in the query string:

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `write`-scope project access token.

### Body Parameters

The following params must be supplied as JSON, and as the body of the request. Be sure to set the header `Content-Type: application/json`.

Name | Type | Description
-----|------|-------------
`status`|`string`|**Required.** Valid values: `active`, `resolved`, `muted`
`resolved_in_version`|`string`|If not empty, a string up to 40 characters describing the version that the item was resolved in. Only used if `status` is set to `resolved`.

### Examples

Mark item `275123456` as resolved:

```
curl -X PATCH 'https://api.rollbar.com/api/1/item/275123456?access_token=abcd1234abcd1234' \
  --header "Content-Type: application/json" \
  --data '{"status": "resolved"}'
```


-----

Last updated: May 12, 2014
