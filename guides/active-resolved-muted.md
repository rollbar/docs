In Rollbar, all Items have a *status* that determines where they appear
and how they behave. There are three statuses: Active, Resolved, and
Muted.

### Active

![](http://photos.osmek.com/Screenshot-2014-11-18-122008.140812.o.png)

All items start as Active. In the Active state:

-   The item can appear on the Dashboard
-   Notifications will be triggered on the first occurrence and when
    thresholds are crossed (according to notification rules)
-   Occurrences count for billing purposes

The Active state is intended to represent an ongoing type of event
happening in your application. It could represent a bug that has not yet
been fixed, or an intermittent ongoing backend issue.

Items can change from Active to Resolved in these ways:

-   Manually changed by a user in the Rollbar UI (by pressing "Resolve"
    or "Set Status" -> "Resolved")
-   Set via the [Rollbar API](https://rollbar.com/docs/api/items/#modify-an-item)
-   [Resolved via commit message](https://rollbar.com/docs/resolve-via-commits/) when that
    commit is deployed
-   Autoresolved on deploy, when enabled (see Settings -> Deploys)
-   Autoresolved after not occurring for a period of time, when enabled
    (see Settings -> Cleanup)

Items can change from Active to Muted in these ways:

-   Manually changed by a user in the Rollbar UI (by pressing "Mute" or
    "Set Status" -> "Muted")
-   Set via the [Rollbar API](https://rollbar.com/docs/api/items/#modify-an-item)

### Resolved

![](http://photos.osmek.com/Screenshot-2014-11-18-122204.140813.o.png)

Resolved items represent issues that are believed to be fixed. In the
Resolved state:

-   The item won't appear on the Dashboard
-   If the item occurs again in a newer version of the code (or no
    version was specified), it will be "Reactivated". This will will
    trigger a notification.
-   Occurrences count for billing purposes

When you believe you have fixed a bug, or if you want to be notified the
next time it happens, mark it as Resolved.

If possible, you should include the version that it is resolved in: this
will prevent it from being reactivated before you deploy the new code,
or from being reactivated by clients that are still running the old code
(this is especially important for mobile apps). Note that this
functionality requires the 'code\_version' to be configured in the
notifier. More details in [this post](https://rollbar.com/blog/resolving-rollbar-items-in-versions).

Items can change from Resolved to Active in these ways:

-   Manually changed by a user in the Rollbar UI (by pressing "Reopen"
    or "Set Status" -> "Active")
-   Set via the [Rollbar API](https://rollbar.com/docs/api/items/#modify-an-item)
-   Automatically on the next occurrence of the same item (subject to
    the version constraint described above)

Items can change from Resolved to Muted in these ways:

-   Manually changed by a user in the Rollbar UI (by pressing "Reopen")
-   Set via the [Rollbar API](https://rollbar.com/docs/api/items/#modify-an-item)

### Muted

![](http://photos.osmek.com/Screenshot-2014-11-18-122244.140814.o.png)

Muted items represent issues that are not currently worth
investigating. In the Muted state:

-   The item won't appear on the Dashboard
-   If the item occurs again, it will remain Muted
-   Occurrences count for billing purposes

If you have an item that you consider a non-issue, or otherwise don't
plan to do anything about soon, you can Mute it so it stays out of
sight.

Muted items are still indexed, searchable, etc. and can be changed back
to Active at any time. For this reason, occurrences of Muted items do
count for billing purposes. If you need to reduce your usage, you should
set a [rate limit](https://rollbar.com/docs/rate-limits/) or filter it
before it is sent to Rollbar.

Items can change from Muted to Active in these ways:

-   Manually changed by a user in the Rollbar UI (by pressing "Unmute"
    or "Set Status" -> "Muted")
-   Set via the [Rollbar API](https://rollbar.com/docs/api/items/#modify-an-item)

Items can change from Muted to Resolved in these ways:

-   Manually changed by a user in the Rollbar UI (by pressing "Set
    Status" -> "Resolved")
-   Set via the [Rollbar API](https://rollbar.com/docs/api/items/#modify-an-item)
