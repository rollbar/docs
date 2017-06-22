# Merging Items

Item merging allows you to combine multiple items into one 'group' for easier management and more accurate metrics.  All past and future occurrences of any merged items will automatically be combined.

## Merge into a new item

The first time you encounter a duplicated error, you'll want to create a new group:

* Select one or more items from the same environment in the Items feed.  An action bar will appear at the top of the screen.
* Slide the toggle to Merge, set appropriate `Level`, `Status`, `Owner`, and `Source` values, type in a name for the new item, and click the Merge button.

## Merge into an existing item

Often times you will see a new error that should be merged with an existing group.  To do this:

* Select the item(s) that should be merged, then switch the toggle to 'Merge'.
* In the text box, click the Search button, then start typing in the name or number (e.g. `#123`) of the existing item, and then select the item from the result list and click 'Merge'.

NOTE:  If you decide to create a new item rather than merging into an existing item, simply click the pencil icon and type a name for the new item.

## Un-merge items

If you want to remove items from a group (e.g. because you mistakenly merged the wrong items):

* Go to the group item and select the 'Member Items' tab at the bottom of the screen to view all items which have been merged into it.
* Select the items you want to remove and click 'Un-merge'.

## Search for merged items
By default, items which have been merged into a group will no longer appear in the project item feed.  To view these items, you can search for `is:member`.

To filter the item feed to only show group items, you can search for `is:group`.

## Automatically merge similar items

After you've merged to create a group item, all future occurrences with the same [fingerprint](../grouping-algorithm/) as one of the member items will be included into the group.  You may also want to merge _similar_ items that will have different fingerprints into the same group (e.g. all `TimeoutError` exceptions regardless of where they occur).

In order to do this, you can set up a [custom fingerprinting rule](../custom-grouping/) that assigns future occurrences to the group item.  The following example will assign all future occurrences with exception class `TimeoutError` to the existing group item `#123:

```json
[
  { "condition": {"path": "body.trace.exception.class", "eq": "TimeoutError"},
    "fingerprint": "group-item-123"
  }
]
```
