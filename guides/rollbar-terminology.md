Rollbar has some unique terms for talking about errors you send us. 

### Item

If you send an error to Rollbar that has not been sent to Rollbar before, an item is created. This can be viewed in your project's item view, and at links such as `https://rollbar.com/<account_name>/<project_name>/items/<item_number>/`.

### Counter

The counter is the same as the `<item_number>` in the above link. It is essentially the reference number for the item. Counter is a term that is only used for accessing items [via our API](https://rollbar.com/docs/api/items/#get-an-item-by-counter).

### Occurrence

An occurrence is an individual occurrence of an item. When a new item is sent to Rollbar, both an item and an occurrence are created. If the same error with the same stacktrace is sent to Rollbar, another occurrence is created for it, but no new item is created. Individual occurrences are available to view in the "Occurrences" tab in an item view, as well as at links such as `https://rollbar.com/<account_name>/<project_name>/items/<item_number>/occurrences/<occurrence_number>/`. 

For information about how occurrences are grouped together, [see the docs](https://rollbar.com/docs/grouping-algorithm/) on our grouping algorithm. If you'd like to change how occurrences are grouped according to your own specified criteria, you can set up [custom grouping rules](https://rollbar.com/docs/custom-grouping/).

### Resolved/Reactivated/Reopened Items

Items that are resolved are believed to be fixed. Items can change from Active to Resolved in these ways:

-   Manually changed by a user in the Rollbar UI (by pressing "Resolve"
    or "Set Status" -> "Resolved")
-   Set via the [Rollbar API](https://rollbar.com/docs/api/items/#modify-an-item)
-   [Resolved via commit message](https://rollbar.com/docs/resolve-via-commits/) when that
    commit is deployed
-   Autoresolved on deploy, when enabled (see Settings -> Deploys)
-   Autoresolved after not occurring for a period of time, when enabled
    (see Settings -> Cleanup)

 If the item occurs again in a newer version of the code (or no version was specified), it will be "Reactivated". If a user manually reopens an item that was resolved or it occurs again in the same version of the code, it will be "Reopened".