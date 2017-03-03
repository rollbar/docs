# Custom Grouping

If our [default grouping algorithm](https://rollbar.com/docs/grouping-algorithm/) is separating occurrences that you would rather have grouped together, or grouping occurrences together you would rather have separated, you can set up Custom Grouping Rules.

To set your custom grouping rules, go to **Settings -> Grouping** for the project you want to configure.

Here's an example configuration:

```json
[
  {"condition": {"path": "body.trace.exception.class", "eq": "TimeoutError"},
    "fingerprint": "timeout-error",
    "title": "Timeout Error"
  },
  {"condition": {"path": "body.trace.exception.class", "eq": "IndexError"},
    "fingerprint": "index-error",
    "title": "Index Error"
  }
]
```

The above configuration is a list of rules. Each rule is a JSON object that consists of a
`condition`, a `fingerprint`, and a `title`. 

Rules are applied in order, testing the `condition` against the incoming occurrence. If a match is
found, the rule's `fingerprint` and `title` will be used instead of our [default grouping algorithm](/docs/grouping-algorithm/).

Occurrences with the same `fingerprint` are grouped together into an _Item_. 

The `title` of the first occurrence of an Item is used as the title of the Item, and is only changed if the item is resolved and then later reactivated. Upon reactivation, the title of the reactivating occurrence is used as the new Item title.

### Condition

The `condition` is defined as a single JSON object. It can either be:

-   a leaf condition, having a `path` key and an operator key (see list
    below).
-   a branch condition, having a single key named `any`, `all`, or
    `none`, whose value is a list of other conditions.

The `path` describes a path from the root of the occurrence data to the
data that the condition tests. Use dots (`.`) to select object
properties or array elements. You can also use the `*` character in
place of an array index or property name to select all matching
elements; in this case, the condition will pass if the operator
evaluates to true for *any* of the matching elements.

Here are a few useful paths:

| `body.trace.exception.class` | Exception class name
| `body.trace.exception.message` | Exception message
| `body.trace.frames.0.filename` | Filename of the first stack frame
| `body.trace.frames.-1.filename` | Filename of the last stack frame
| `body.trace.frames.\*.filename` | Filename of any stack frame
| `body.trace.frames.\*.method` | Method/function name of any stack frame
| `language` | The language name

Much more is available; you can use any of the data in the occurrence
payload. The exact elements available vary by library; right now the
best way to see what's available is to read the source code of your
library, inspect an actual instance using our API, or read the
[Items API docs](https://rollbar.com/docs/api/items/).

The following operators are available:

| `eq` | Equals
| `neq` | Not Equals
| `in` | Contained in the string or list
| `nin` | Not contained in the string or list
| `contains` | Contains the string, element, or key
| `ncontains` | Does not contain the string, element, or key (or is not a string, array, or object)
| `gt` | Greater than
| `gte` | Greater than or equal to
| `lt` | Less than
| `lte` | Less than or equal to

For the numeric operators (`gt`, `gte`, `lt`, `lte`): the right side must be a
number, and the left side (data from the occurrence) will be coerced to
a number, defaulting to 0.

**Example:** Match items whose exception class is NameError

```json
{
  "path": "body.trace.exception.class",
  "eq": "NameError"
}
```

**Example:** Match items whose exception class is TypeError or
ValueError, and exception message contains the string "database"

```json
{
  "all": [
    { "any": [
      { "path": "body.trace.exception.class", "eq": "TypeError" },
      { "path": "body.trace.exception.class", "eq": "ValueError" }
    ]},
    { "path": "body.trace.exception.message", "contains": "database" }
  ]
}
```

Note: If your exception has nested stack traces, rather than using `body.trace.exception.message`, you'll need to use `body.trace_chain.0.exception.message`, and so on for any paths that begin with `body.trace`. 

### Templating

Both `fingerprint` and `title` can contain template markers (wrapped in
`{{ double_braces }}`) as well as hardcoded strings.

There are two special markers:

-   `{{ default_fingerprint }}`: will be replaced with the fingerprint
    hash calculated by our default algorithm.
-   `{{ default_title }}`: will be replaced with the title calculated by
    our default algorithm.

These can be used to tune the grouping algorithm without entirely
replacing it.

Additionally, any part of the occurrence JSON body may be referenced by
path. For example, `{{ body.trace.exception.class }}` will be replaced
with the exception class. You can combine this with static text or the
special markers achieve many kinds of grouping.

### Fingerprint

Occurrences with the same `fingerprint` are grouped together into an Item.

### Title

The `title` is a text description that is displayed when viewing an item.  It must be a string, of length 1-255 characters. You can change the title in this configuration without affecting grouping. The new title will take effect if the item is reactivated after being resolved.

### Complete Example

Here's an example complete configuration with three rules.

```json
[
  { 
    "condition": {
      "path": "body.trace.exception.class",
      "in": ["EOFError", "Errno::ECONNREFUSED", "Errno::ETIMEDOUT"]
    },
    "fingerprint": "connection-error",
    "title": "Connection error"
  },
  { 
    "condition": {"all": [
      {"path": "body.trace.exception.class", "eq": "TimeoutError"},
      {"path": "body.trace.frames.*.filename", "contains": "payments"}
    ]},
    "fingerprint": "payments-timeout-error",
    "title": "Timeout error in payments code"
  },
  {
    "condition": {
      "path": "body.trace.exception.class",
      "eq": "ActionController::RoutingError"
    },
    "fingerprint": "{{ default_fingerprint }}-{{ context }}",
    "title": "{{ default_title }} in {{ context }}"
  }
]
```
