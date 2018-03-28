---
title: Using UUIDs
---

# UUIDs

The Rollbar API supports including a UUID with occurrence reports which
can later be used to look up that exact occurrence. UUIDs are generated
by the client library, not returned from the API. A few use-cases
include:

-   Showing a UUID on your custom error pages, so your users can give it
    to you when they contact your support channels
-   The "View in Rollbar" links in the official Django and Pyramid
    libraries
-   The "Details:" link in the official Ruby gem

### Using a UUID

If you have a UUID—for example, that you've been given by one of your
users—you can use it to go directly to either the related Item or the
related Occurrence. Assuming a UUID of
`aaaaaaaa-bbbb-cccc-dddd-eeeeffffeeee`:

-   The related Item can be found at
    `https://rollbar.com/item/uuid/?uuid=aaaaaaaa-bbbb-cccc-dddd-eeeeffffeeee`
-   The related Occurrence can be found at
    `https://rollbar.com/occurrence/uuid/?uuid=aaaaaaaa-bbbb-cccc-dddd-eeeeffffeeee`

The above links will redirect to the appropriate places on Rollbar as
long as:

-   The occurrence has been processed by our processing pipeline. This
    usually takes less than 5 seconds, but occasionally the delay gets
    longer. If the delay exceeds 1 minute, this will be reported in the
    dashboard.
-   The occurrence was reported to Rollbar in the first place.

If the link doesn't redirect at first, try waiting a few seconds and
hitting Refresh. If the link still is not redirecting after 1 minute,
and there is no processing delay reported in the dashboard, it's likely
that something prevented it from being reported to Rollbar in the first
place. Check your server logs for more details, and feel free to contact
<support@rollbar.com> for help debugging.

### UUID Bookmarklet

To easily look up items via UUID, create this handy little bookmarklet. 
Simply create a bookmark, name it RollbarUUID, and add the following code as the URL.
Then the next time you get a UUID (in an email or on a site), just highlight it, click the bookmark, and you will be redirected to the occurrence.

```javascript
javascript:(function(){function selectedText() {var text = "";if (window.getSelection) {text = window.getSelection().toString();} else if (document.selection && document.selection.type != "Control") {text = document.selection.createRange().text;}return text;}var url = "https://rollbar.com/occurrence/uuid/?uuid=" + selectedText();var win = window.open(url, '_blank');win.focus();})();
```
