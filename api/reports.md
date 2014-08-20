# Reports

This collection of API calls allows access to the same kind of reports as on the Dashboard in the UI.

These calls require a project-level access token with `read` scope, which should be provided in the query string. The prefix for all URLs is `https://api.rollbar.com`


<!-- Sub:[TOC] -->

----

## Fetch the top recent active items

Analogous to the "Top 10 items in last 24 hours" report on the Dashboard.

    GET /api/1/reports/top_active_items

### Parameters

Name | Type | Description
-----|------|------------
`hours`|`integer`|Number of recent hours to consider. Min 1, max 168, default 24. Optional.
`environments`|`string`|Comma-separated list of environments to consider. Optional; empty means "any environment"

### Response

Response is JSON.

```javascript
{
  "err": 0,
  "result": [
    // each element in the list is an object with an "item" object and a "counts" list
    {
        // data describing the item (similar to that returned by GET /api/1/item/:id)
        "item": {
            "id": 2071,
            "counter": 1007,
            "environment": "production",
            "framework": 0,
            "last_occurrence_timestamp": 1408410581,
            "level": 40,
            "occurrences": 54,
            "project_id": 12345,
            "title": "Something went wrong",
            "unique_occurrences": 5
        },
        // list of occurrence counts in the past 24 hours. Oldest first.
        "counts": [12, 10, 7, 3, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 2, 8, 5, 6]
    },
    { /* more elements ... */ }
  ]
}
```


-----

Last updated: August 19, 2014

