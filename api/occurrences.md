# Occurrences

These calls require a project-level access token, which should be provided in the query string. The prefix for all URLs is `https://api.rollbar.com`

Quick note: the URLs use the term 'instance', rather than 'occurrence', for backwards-compatibility reasons.

<!-- Sub:[TOC] -->

---

## Get an occurrence by ID

Returns a JSON object describing the occurrence. This is similar to the "Raw JSON" section of the occurrence detail page.

    GET /api/1/instance/:id

`:id` must be an Occurrence ID for an occurrence in the project. These IDs are returned as the `id` field in other occurrence API calls, and can be found in the Rollbar UI on URLs like "https://rollbar.com/Rollbar/demo/items/54/occurrences/3209095494/" (3209095494 is the Occurrence ID).


### Query String Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `read`-scope project access token.


---

## List all occurrences

Returns all occurrences in the project, in pages of 20. Order is descending by occurrence ID (which is approximately descending by timestamp).

    GET /api/1/instances/


### Query String Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `read`-scope project access token.
`page`|`integer`|Page number, starting from 1. 20 occurrences are returned per page.


---

## List all occurrences of an item

Returns all occurrences of an item, in pages of 20. Order is descending by occurrence ID (which is approximately descending by timestamp).

    GET /api/1/item/:item_id/instances/

`:id` must be an Item ID for an item in the project. These IDs are returned as the `id` field in the other Item API calls.


### Query String Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `read`-scope project access token.
`page`|`integer`|Page number, starting from 1. 20 occurrences are returned per page.


---

## Delete an occurrence

Permanently deletes an occurrence. This will make it unavailable in the Rollbar UI and API. Aggregate counts are not updated.

    DELETE /api/1/instance/:id

Requires `write` scope.

`:id` must be an Occurrence ID for an occurrence in the project. These IDs are returned as the `id` field in other occurrence API calls, and can be found in the Rollbar UI on URLs like "https://rollbar.com/Rollbar/demo/items/54/occurrences/3209095494/" (3209095494 is the Occurrence ID).

### Query String Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required.** A `write`-scope project access token.

### Example

Delete occurrence `3208965626`:

```
curl -X DELETE 'https://api.rollbar.com/api/1/instance/3208965626?access_token=abcd1234abcd1234'
```

Response:

```
{
  "err": 0,
  "message": "The instance has been deleted"
}
```

-----

Last updated: November 13, 2014
