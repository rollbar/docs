## Connecting Rollbar to Datadog

Are you new to Rollbar?
[If so, click here to learn more about Rollbar and sign up!](https://rollbar.com/)
{: .info}

Improve your monitoring and connect Rollbar to Datadog. Rollbar users can syndicate exceptions,
errors and code deployments as 'Events' in [Datadog](https://www.datadoghq.com/). Installation
instructions below.

### Setup

Configuration is per-project in Rollbar.

1. On Datadog, head to the APIs page to get your API Key (copy to your clipboard): Integrations → APIs.
   ![](https://d26gfdfi90p7cf.cloudfront.net/rollbar-datadog-keys.152870.l.png)

2. In Rollbar, go to the Notification settings page for a project: Dashboard → Settings →
   Notifications → Datadog.
   ![](https://d26gfdfi90p7cf.cloudfront.net/rollbar-datadog.152871.l.png)

3. Add your Datadog API key.
   ![](https://d26gfdfi90p7cf.cloudfront.net/rollbar-datadog-integration.152873.l.png)

4. Click Enable Datadog Integration

Congrats! Datadog is now integrated with Rollbar. Once integrated, the default notification 'Rules'
will be activated and sent to your Datadog account.

![](https://d26gfdfi90p7cf.cloudfront.net/notification-rules-rollbar.152867.l.png)

Tip: Click Edit to customize notification 'Rules' settings and formatting.
{: .info}

![](https://d26gfdfi90p7cf.cloudfront.net/datadog-rule-edit.152876.o.png)
