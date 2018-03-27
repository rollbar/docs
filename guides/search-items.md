---
title: Searching Items
---

# Searching Items

On the Items view, you can filter your Items by many different properties. Some properties are
direct properties of the items themselves, while others are evaluated against the occurrences of the
item.

In all cases, the Items search will return the matching items and the properties about those items.
For filters that evaluate against occurrences, except as noted below, the aggregate statistics shown
for each Item describe the Item as a whole (not the subset of occurrences that match the search).

### Filters built into the UI

Level
: Filters items by current level. Critical, Error, Warning, Info, Debug. Click on/off to choose
  any or all.
 
Owner
: Filters items based on assigned owner. Find items assigned to a specific project member, _any_ project member, or unassigned.

Status
: Filters items by current status. Active, Resolved, Muted or Any Status.

Environment
: Filters items by environment. Auto-populated based on the data in the project. Any Environment,
  or choose an environment.

Source
: Filters items by source. Auto-populated based on the data in the project, and only appears when
  there is more than one source (i.e. language/framework). Any Source, or choose a source.

Seen
: Finds items that had at least one occurrence in the specified date range. Aggregate counts shown
  do reflect the occurrences in the specified date range.

Activated
: Finds items that were activated (first seen, or reactivated after being resolved) in the specified
  date range.

### Search commands

Many more search options are available via the text box.

Title
:  `hello world` finds items whose title contains both "hello" and "world" (infix search).

Server Host
: `host:web` finds items that occurred at least once on a host whose name starts with "web". Host filters impact the occurrence count, causing it to count only the occurrences from the specified host.
  (prefix search)

Context
: `context:home#index` finds items with context matching "home#index" (prefix search).

Comments
: `has:comments` finds items that have comments.

IP Address
: `ip:101.102.103.104` finds items that were seen by the ip address "101.102.103.104" (exact match).

People
: `user_id:12345` finds items/people associated with the user id "12345".
: `username:snowden` finds items/people associated with the username "snowden".
: `email:dvader@theempire.org` finds items/people associated with the email "dvader@theempire.org".
: `user_id:`, `username:` and `email:` searches default to prefix searches unless an explicit suffix
  search is made.
: e.g. searching for `username:alice` will return alice, alice1234, aliceasdf.
: e.g. searching for `username:*alice` will not return alice1234, aliceasdf.
: e.g. searching for `username:"alice"` will perform an exact match search.

Stack Trace
: `file:index.php` finds items with stack traces with at least one filename containing "index.php".
: `topfile:mydomain.com` finds items where the topmost stack frame contains "mydomain.com".
: `bottomfile:mydomain.com` finds items where the bottommost stack frame contains "mydomain.com".
: `allfiles:mydomain.com` finds items where all stack trace filenames contain "mydomain.com".
: `nofiles:evildomain.com` finds items where no stack trace filenames contain "evildomain.com".
: `minfiles:2` finds items with at least 2 filenames in the stack trace.
: `maxfiles:10` finds items with at most 10 filenames in the stack trace.

Code Version
: `code_version:abcdef` finds items that have been seen in the code_version `abcdef`.

Item Number
: `#123` finds the item with counter number `123`

Merging
: `is:group` finds group items that were created by merging similar items
: `is:member` finds items that have been merged into a group

Fingerprint
: `fingerprint:my-custom-fingerprint` finds items that have the fingerprint `my-custom-fingerprint` (exact match, useful in conjunction with Custom Grouping or sending your own fingerprint string).
