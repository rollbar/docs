Rollbar has some unique terms for talking about errors you send us. 

### Item

If you send an error to Rollbar that has not been sent to Rollbar before, an item is created. This can be viewed in your project's item view, and at links such as `https://rollbar.com/<account_name>/<project_name>/items/<item_number>/`.

### Counter

The counter is the same as the `<item_number>` in the above link. It is essentially the reference number for the item. Counter is a term that is only used for accessing items [via our API](https://rollbar.com/docs/api/items/#get-an-item-by-counter).

### Occurrence

An occurrence is an individual occurrence of an item. When a new item is sent to Rollbar, both an item and an occurrence are created. If the same error with the same stacktrace is sent to Rollbar, another occurrence is created for it, but no new item is created. Individual occurrences are available to view in the "Occurrences" tab in an item view, as well as at links such as `https://rollbar.com/<account_name>/<project_name>/items/<item_number>/occurrences/<occurrence_number>/`.

### Resolved/Reactivated/Reopened Items

Items that are resolved are believed to be fixed. If the item occurs again in a newer version of the code (or no version was specified), it will be "Reactivated". If a user manually reopens an item that was resolved or it occurs again in the same version of the code, it will be "Reopened".