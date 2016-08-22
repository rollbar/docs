Every occurrence in Rollbar has a timestamp. The timestamps that you see
throughout the Rollbar UI and API are the according to Rollbar's
servers. We use and continuously
monitor [ntpd](http://en.wikipedia.org/wiki/Ntpd) to keep our clocks in
sync.

Timestamps are stored internally as unix timestamps, at second-level
precision.

Timestamps that are displayed in human-readable form use the timezone
configured at the project level. This ensures that everyone on your
team, even if distributed, sees the same absolute timestamps.

Timestamps returned from the [API](../../../docs/api_overview/) are unix
timestamps, as are timestamps in [RQL](../../docs/rql/) queries.

The original timestamp reported to Rollbar by your application is
available in the field `metadata.customer_timestamp`. It will normally
be a unix timestamp as well. You can see this in two places:

1.  <span style="line-height: 1.5em;">On the occurrence detail page, the
    Raw JSON section will include a `metadata` section. If there was a
    timestamp in the original report, it will be present as the key
    `customer_timestamp`.</span>
2.  <span style="line-height: 1.5em;">Via RQL, you can select it as the
    column name `metadata.customer_timestamp`</span>
