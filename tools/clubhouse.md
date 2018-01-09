# Create Clubhouse Stories from Rollbar

For general information about Rollbar's issue tracking features, check out the [Issue Tracking guide](../issue-tracking/). 
{: .info}

## In Clubhouse

* Go to **Settings -> API Tokens**, generate a new API token named 'Rollbar', and copy it. 

## In Rollbar

* Go to **User Settings -> Connected Account -> Clubhouse** and save your Clubhouse API token.
* In your Rollbar project, go to **Settings -> Notifications** and then select Clubhouse from the list of available channels.
* In the Clubhouse configuration screen enter/select the following:
   * API Token:  Select a token to use as the default for automatic story updates
   * Organization:  Enter the name of your organization, found at `https://app.clubhouse.com/{organization}/`.
   * Clubhouse project:  The project where stories will be created
   * Reactivated state:  Clubhouse workflow state in which stories will be placed if a linked Rollbar item is reactivated.
   * Resolved state: Clubhouse workflow state in which stories will be placed if a linked Rollbar item is resolved.
* Click **Save Settings**, then click **Send Test Notification** to verify that stories can be created.

For detailed instructions on using and configuring automatic and manual issue tracking integration, check out the Issue Tracking guide. {: .info} 
