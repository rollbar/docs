# Custom Fingerprinting Rules

If our [default fingerprinting algorithm](https://rollbar.com/docs/grouping-algorithm/) is separating occurrences that you would rather have combined or vice versa, then you can set up Custom Fingerprinting Rules.

To set your custom grouping rules, go to **Settings -> Custom Fingerprinting** for the project you want to configure.

Here's an example configuration:

```json
[
  {"condition": {"path": "body.trace.exception.class", "eq": "TimeoutError"},
    "fingerprint": "timeout-error",
    "title": "Timeout Error"
  },
  {"condition": {"path": "body.trace.exception.class", "eq": "IndexError"},
    "fingerprint": "index-error"
  }
]
```

The above configuration is a list of rules. Each rule is a JSON object that consists of a
`condition`, a `fingerprint`, and an optional `title`. 

Rules are applied in order, testing the `condition` against the incoming occurrence. If a match is
found, the rule's `fingerprint` and `title` will be used instead of our [default algorithm](/docs/grouping-algorithm/).

Occurrences with the same `fingerprint` are combined into an _Item_. 

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

#### Path

Here are a few commonly used paths:

| `body.trace.exception.class` | Exception class name
| `body.trace.exception.message` | Exception message
| `body.trace.frames.0.filename` | Filename of the first stack frame
| `body.trace.frames.-1.filename` | Filename of the last stack frame
| `body.trace.frames.\*.filename` | Filename of any stack frame
| `body.trace.frames.\*.method` | Method/function name of any stack frame
| `language` | The language name

You can use any value in your JSON payload as a path, including custom data.  To view your JSON payloads, go into an occurrence and click on **View JSON** at the bottom of the screen.

Here's a simple example of some error JSON:

```json
{
  "body": {
    "trace": {
      "frames": [
        {
          "method": "HTMLDocument.e._wrapped", 
          "lineno": 32, 
          "colno": 100, 
          "filename": "https://cdnjs.cloudflare.com/ajax/libs/rollbar.js/1.9.3/rollbar.min.js"
        }
      ], 
      "exception": {
        "message": "Boomerang is not defined", 
        "class": "ReferenceError", 
        "description": "Error while initializing Heroku header"
      }
    }
  },
  "server": {
    "host": "web01"
  }
}
```
In this example, the value of `body.trace.frames.0.lineno` is `32`, and the value of `server.host` is `web01`. 

#### Operators

The following operators are available:

| `eq` | Equals |
| `neq` | Not Equals |
| `in` | Contained in the string or list |
| `nin` | Not contained in the string or list |
| `contains` | Contains the string, element, or key |
| `ncontains` | Does not contain the string, element, or key (or is not a string, array, or object) |
| `gt` | Greater than |
| `gte` | Greater than or equal to |
| `lt` | Less than |
| `lte` | Less than or equal to |

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

### Fingerprint

Occurrences with the same `fingerprint` are combined into an Item.  To add occurences to an existing group item created by [manual merging](../merge-items/), use the fingerprint `group-item-###`, e.g. `group-item-123`.  See the [merging guide](../merge-items/#automatically-merge-similar-items) for an example.

### Title

The `title` is an optional text description that is displayed when viewing an item.  It must be a string, of length 1-255 characters. You can change the title in this configuration without impacting the fingerprint. The new title will take effect if the item is reactivated after being resolved.

### Templates

Both `fingerprint` and `title` can contain template markers (wrapped in
`{{"{{double braces"}}}}`) as well as hardcoded strings.

There are two special markers:

-   `{{"{{default_fingerprint"}}}}`: will be replaced with the fingerprint
    hash calculated by our default algorithm.
-   `{{"{{default_title"}}}}`: will be replaced with the title calculated by
    our default algorithm.

These can be used to tune the fingerprinting algorithm without entirely
replacing it.

Additionally, any part of the occurrence JSON body may be referenced by path.  For example 

- `{{"{{ body.trace.exception.class "}}}}` will be replaced
with the exception class.
- `{{"{{ body.trace.exception.message "}}}}` will be replaced with the exception message.

You can combine this with static text or the special markers achieve many kinds of fingerprinting.

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
      {"path": "body.trace.frames.\*.filename", "contains": "payments"}
    ]},
    "fingerprint": "payments-timeout-error",
    "title": "Timeout error in payments code"
  },
  {
    "condition": {
      "path": "body.trace.exception.class",
      "eq": "ActionController::RoutingError"
    },
    "fingerprint": "{{"{{ default_fingerprint "}}}}-{{"{{ context "}}}}",
    "title": "{{"{{ default_title "}}}} in {{"{{ context "}}}}"
  }
]
```
