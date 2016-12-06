Important: RQL is a work in progress. While it's generally stable,
expect bugs at the corners.

### Overview

RQL ("Rollbar Query Language") is an attempt at exposing a rich querying
interface to the data in Rollbar. Its goal is to be SQL-like, so it
should be familiar to SQL users.

This first release allows running `SELECT`s on two logical tables,
`item_occurrence` and `deploy`. Basic GROUP BY, ORDER BY, LIMIT, and
aggregation functions all work, as do arbitrary expressions in the WHERE
clause. No DISTINCT, HAVING, subqueries, or joins yet.

### Syntax

Simple-ish queries are supported. SELECT, FROM, and WHERE are required.
GROUP BY, ORDER BY, and LIMIT are optional.

`SELECT *` \*may\* be used (as long as there is no GROUP BY). It will
return a list of columns similar to the Occurrences tab on Item Detail
pages.

SQL keywords and built-in function names are case-insensitive (i.e.
`SELECT` and `select` are both fine).

Names (i.e. column names) should start with a lowercase letter and may
contain letters, numbers, and periods (for specifying a JSON path). If
you need any other characters (i.e. a hyphen, or to start with an
uppercase letter), escape with backticks (i.e.
`` `request.headers.User-Agent` ``)

#### Operators

-   `+`, `-`, `/`, `*`, `DIV`, `MOD`
-   `AND`, `OR`, `NOT`
-   `=`, `!=`,
    `<>`, `>`, `>=`, `<`, `<=`, `IN`, `NOT IN`, `BETWEEN`,
    `NOT BETWEEN`, `LIKE`, `NOT LIKE`

#### Built-in Functions

-   `count(*)`: counts all rows
-   `count(foo)`: counts rows where foo is not null
-   `sum(foo)`: sums value of foo (for rows where not null)
-   `avg(foo)`: average value of foo (for rows where not null)
-   `min(foo)`: minimum value of foo
-   `max(foo)`: maximum value of foo
-   `unix_timestamp()`: returns the current unix timestamp, as an
    integer
-   `concat(str1, str2, ...)`: returns the string resulting from
    concatenating all arguments
-   `concat_ws(sep, str1, str2, ...)`: returns the string resulting from
    concatenating the second argument and beyond, separated by the first
    argument
-   `lower(str)`: converts str to lowercase
-   `upper(str)`: converts str to uppercase
-   `left(str, len)`: returns the len leftmost characters of str
-   `right(str, len)`: returns the len rightmost characters of str
-   `substring(str, pos)`: returns the substring from str starting at
    pos (all characters from pos until the end)
-   `substring(str, pos, len)`: returns a substring from str starting at
    pos, at most len characters
-   `locate(substr, str)`: returns the position of the first occurrence
    of substr in str. (1-indexed)
-   `locate(substr, str, pos)`: returns the position of the first
    occurrence of substr in str, starting the search at position pos
-   `char_length(str)`: returns the length of str in characters
-   `length(str)`: returns the length of str in bytes

### Examples

```sql
SELECT request.user_ip, min(timestamp), max(timestamp), count(*)
FROM item_occurrence
WHERE item.counter = 47
GROUP BY request.user_ip
ORDER BY count(*) DESC
LIMIT 10
```

```sql
SELECT timestamp, body.message.body
FROM item_occurrence
WHERE item.counter BETWEEN 40 AND 50
```

```sql
SELECT *
FROM item_occurrence
WHERE item.counter IN (1,2,3)
```

### Tips

-   Use `SELECT * FROM item_occurrence` to get a display similar to the
    Occurrences tab
-   For better performance, filter by item (i.e.
    `WHERE item.counter = 123`) or by timestamp (i.e.
    `WHERE timestamp > unix_timestamp() - 86400`)
-   When using GROUP BY or ORDER BY, make sure the group/order clause is
    also present in the SELECT clause
-   You can share the URL with a co-worker and they'll see the same
    results you do, without having to run the query again.
-   After a query has completed, press Execute again to re-run it.

### Limitations

-   At most 100 rows will be returned per query (though any number of
    rows may be examined)
-   No `DISTINCT`, `HAVING`, subqueries, joins, or unions
-   No `ANY`, `ALL`, `EXISTS`
-   `SELECT *` cannot be combined with `GROUP BY`
-   Can only be used to examine data within a single project

### Schema

#### item\_occurrence

`item_occurrence` is a table where each row contains data about a single
occurrence, as well as the item that the occurrence is associated with.
Column names starting with "item." reference the item, and all other
column names reference the occurrence. Column names that do not exist in
a particular occurrence evaluate to NULL.

These columns are available under the "item." prefix:

| Name | Description
|-|-
| `item.id` | System-wide ID
| `item.counter` | Project-wide ID
| `item.environment` | Environment name
| `item.platform` | Platform ID
| `item.framework` | Framework ID
| `item.hash` | Fingerprint value
| `item.first_occurrence_id` | ID of the first occurrence
| `item.first_occurrence_timestamp` | Timestamp of the first occurrence
| `item.activating_occurrence_id` | ID of the first occurrence since the item was last resolved
| `item.last_activated_timestamp` | Timestamp the item was last activated
| `item.last_resolved_timestamp` | Timestamp the item was last resolved
| `item.last_muted_timestamp` | Timestamp the item was last muted
| `item.last_occurrence_id` | ID of the most recent occurrence
| `item.last_occurrence_timestamp` | Timestamp of the most recent occurrence
| `item.total_occurrences` | Number of occurrences since last resolved
| `item.last_modified_by` | ID of the user who last modified this item
| `item.status` | Status (active, resolved, muted)
| `item.level` | Level (critical, error, warning, info, debug)
| `item.resolved_in_version` | Revision the item was last resolved in
| `client.javascript.browser` | Raw raw user agent string.

#### deploy

`deploy` is a table where each row represents a single deploy. It has
the following columns:


| Name | Description
|-|-
| `id` | System-wide ID
| `user_id` | Rollbar user\_id of the rollbar\_username recorded for the deploy
| `environment` | Name of the deployed environment
| `revision` | Revision (i.e. git sha or version number) deployed
| `local_username` | Local username recorded for the deploy
| `comment` | The deploy comment
| `timestamp` | Timestamp when the deploy was recorded

### Roadmap

-   "DISTINCT", "HAVING"
-   More performance optimizations
-   More functions
-   Better progress indicators
-   Saved searches
-   More visualization options (i.e. bar graphs, line graphs, etc.)
-   Download results as CSV/JSON dump (with support for large
    resultsets)
-   More data tables

### Known Bugs

-   An aggregation query that does not match any rows will return no
    results at all, instead of a row indicating that zero rows were
    found.
