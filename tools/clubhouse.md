---
title: Integrate Rollbar with Clubhouse
---

# Create Clubhouse Stories from Rollbar

[Clubhouse](https://clubhouse.io/) is a project management tool for software development teams that can be used to track Rollbar items.

For general information about Rollbar's issue tracking features, check out the [Issue Tracking guide](../issue-tracking/). 
{: .info}

## In Clubhouse

* Go to **Settings -> API Tokens**, generate a new API token named 'Rollbar', and copy it to your clipboard. 

## In Rollbar

* Go to **User Settings -> Connected Account -> Clubhouse** and save your Clubhouse API token.
* In your Rollbar project, go to **Settings -> Notifications** and then select Clubhouse from the list of available channels.
* In the Clubhouse configuration screen enter/select the following:
   * API Token:  Token to use as the default for automatic rules.
   * Organization:  Name of your organization, found at `https://app.clubhouse.com/{organization}/`.
   * Clubhouse project:  The project where stories will be created.
   * Clubhouse epic: Epic where the stories will be created. _(Optional)_
   * Initial state:  Clubhouse workflow state in which stories will be placed when created.
   * Reactivated state:  Clubhouse workflow state in which stories will be placed if a linked Rollbar item is reactivated.
   * Resolved state: Clubhouse workflow state in which stories will be placed if a linked Rollbar item is resolved.
   * Labels: Labels to apply to stories when created. _(Optional)_
* Click **Save Settings**, then click **Send Test Notification** to verify that stories can be created with the correct configuration.
* Configure your automated rules, as described in the [Issue Tracking guide](../issue-tracking/).
* Click the toggle to set the integration to **Enabled**.

For detailed instructions on using and configuring automatic and manual issue tracking integration, check out the [Issue Tracking guide](../issue-tracking/).
{: .info} 
