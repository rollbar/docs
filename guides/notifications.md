# Notification Types

Rollbar supports many different [messaging and incident management tools](/docs/tools/#messaging) where your team can get notified about errors and important events.  Notifications can be customized using [variables](/docs/notification-variables) and triggered in specific conditions using [filters](/docs/filtering-notifications).

This page describes the types of notifications you can configure across all available channels.

| Notification Type | Triggered when... |
|-------------------|-------------|
| _New Item_ | An error/ message is seen for the first time. |
| _Every Occurrence_ | Every time an error/ message occurs (_use wisely!_). |
| _10^th Occurrence_ | 10th, 100th, 1,000th, 10,000th, ... occurrence |
| _High Occurrence Rate_ | `{x}` occurrences seen in `{y}` minutes (_configurable_). |
| _Item Resolved_ | An error/message is marked `Resolved`. |
| _Item Reopened_ | An error/message is marked `Active` by a user. |
| _Item Reactivated_ | An error/message occurs again after being marked `Resolved`. |
| _Deploy_ | A new [deploy](/docs/deploy-tracking/) is reported. |
| _Daily Summary_ | _(Available in email only)_ Summary of daily error/message activity in a project |

## Customizing Notifications

Rollbar gives you a great deal of control over when notifications are triggered and how they appear.

* [Notification Filters](/docs/filtering-notifications)
* [Notification Variables](/docs/notification-variables)

## Setup Instructions

### Messaging Apps

* [Slack](/docs/slack/)
* [Hipchat](/docs/hipchat/)
* [Flowdock](/docs/flowdock/)
* [Campfire](/docs/campfire/)

### IT Alerting & Incident Management

* [PagerDuty](/docs/pagerduty)
* [VictorOps](/docs/victorops/)
* [OpsGenie](https://www.opsgenie.com/docs/integrations/rollbar-integration)
* [Datadog](/docs/datadog/)

### Build Your Own

* [Webhooks](/docs/webhooks/)

