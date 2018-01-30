# Environments

Every error reported to Rollbar is required to have an `environment` property.  This value can contain any non-empty alphanumeric string of up to 255 latin-1 characters, so it can be used in a number of ways.

This guide explains a bit about how `environment` is used in the app, some important limitations, and our recommended best practices.

## Important things to know about `environment` in Rollbar:

* `production` is treated as the default environment filter in many Rollbar screens, since we assume that production data matters the most.
* Items cannot be [merged](/docs/merging/) if they are in different environments.
* [Notification rules](/docs/notifications/) can easily be applied to a single environment or all environments, but not necessarily to multiple environments.

## Best practices

* In general, we recommend to have a single `production` environment to enable merging and accurate metrics for all errors that occur in your production systems.
  * For development builds, many customers use the git branch name or the sandbox name as `environment`.  We recommend this approach.
* To track which host an error occurred on, use the `host` property when reporting occurrences (see the docs for your [Rollbar SDK](/docs/notifiers/) for instructions on sending the `host` property.)
  * If all hosts are in the same location, then a `host` format like `web1` is recommended.
  * If hosts are spread across multiple regions / data centers, a format like `us-east1-web1 ` is recommended.
  * Aggregate metrics for hosts can be calculated using [RQL](/docs/rql/), with queries such as the following:
    ```sql
    SELECT server.host, count(*)
    FROM item_occurrence
    WHERE 
    item.environment ='production'
    and item.level >= 40 /* Error or higher */
    and timestamp >= unix_timestamp() - 60*60*24 /* last 24 hours */
    group by 1 
    ```
