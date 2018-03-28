---
title: API Reference - Items (GET, PATCH)
---

# Managing Items

These calls require a project-level access token, which should be provided in the query string.
The prefix for all URLs is `https://api.rollbar.com`


## Get an item by ID

    GET /api/1/item/:id

Requires `read` scope.

`:id` must be an item ID for an item in the project. These IDs are returned as the `id` field in other API calls.

Note that they are NOT found in in URLs like "https://rollbar.com/myaccount/myproject/items/456/" -- that
is the "counter", which can be used in the following API call.



## Get an item by counter

    GET /api/1/item_by_counter/:counter

Requires `read` scope.

`:counter` must be an item counter for an item in the project. The counter can be found in
URLs like "https://rollbar.com/myaccount/myproject/items/456/" (456 is the counter).

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



## List all items

Returns all items in the project, in pages of 100.

    GET /api/1/items/

Requires `read` scope.


### Query String Parameters

Aside from `access_token`, `page`, and `ids`, the query string params are the same as you might
see when using the search functionality on the "Items" part of the Rollbar UI. So you can
copy-paste the query string from the address bar while on the Items page, and use that same query
string in this API call.

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `read`-scope project access token.
`assigned_user`|`string`|If not empty, only items assigned to the specified user will be returned. Must be a valid Rollbar username, or you can use the keywords `assigned` (items that are assigned to any owner) or `unassigned` (items with no owner).
`environment`|`string`|If not empty, only items in the specified environment will be returned. Specify multiple times to filter by multiple environments.
`framework`|`string`|If not empty, only items in the specified framework will be returned. Specify multiple times to filter by multiple frameworks.
`ids`|comma-separated list of integers|If not empty, list of item IDs to return, instead of using all items in the project.
`level`|`string`|If not empty, only items with the specified level will be returned. Valid values: `'debug'`, `'info'`, `'warning'`, `'error'`, `'critical'`. Specifiy multiple times to filter by multiple levels.
`page`|`integer`|Page number, starting from 1. 100 items are returned per page.
`query`|`string`|A query string, using the same format as the search box on the Items page.
`status`|`string`|If not empty, only items with the specified status will be returned. Valid values: `'active'`, `'resolved'`, `'muted'`. Specify multiple times to filter by multiple statuses.

### Examples

Get the 101st through 199th active items:

```bash
curl 'https://api.rollbar.com/api/1/items/?access_token=abcd5678&status=active&page=2'
```

Get the first page of items that are error or critical, in the production environment:

```bash
curl 'https://api.rollbar.com/api/1/items/?access_token=abcd5678&level=error&level=critical&environment=production'
```



## Modify an item

    PATCH /api/1/item/:id

Used to modify an item's state. Currently supports:

- setting the status, level, title, assigned user
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
`status`|`string`|If present, the new status. Valid values: `active`, `resolved`, `muted`
`resolved_in_version`|`string`|If not empty, a string up to 40 characters describing the version that the item was resolved in. Only used if `status` is set to `resolved`.
`level`|`string`|If present, the new level. Valid values: 'critical', 'error', 'warning', 'info', 'debug'
`title`|`string`|If present, the new title. Should be a string with length 1 to 255.
`assigned_user_id`|`int`|If present, the new assigned user ID. Valid values are `null` or any user ID with access to this item.

### Examples

Mark item `275123456` as resolved in version `aabbcc1`:

```bash
curl -X PATCH 'https://api.rollbar.com/api/1/item/275123456?access_token=abcd1234abcd1234' \
  --header "Content-Type: application/json" \
  --data '{"status": "resolved", "resolved_in_version": "aabbcc1"}'
```


