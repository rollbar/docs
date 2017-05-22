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
