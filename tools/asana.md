# Connecting Asana to Rollbar

Turn application errors in your [Rollbar](https://rollbar.com/) projects into Tasks in your
[Asana](https://asana.com/) Projects.

## Authorize Rollbar

In order to create tasks in your Asana account, at least one user in your Rollbar account must authorize Rollbar to access Asana.
{: .info}

* Click on your avatar and select **User Settings**.
* Click on **Connected Accounts** and select 'Asana'.
* Click on **Connect to Asana** and then complete the authorization flow.  

Once you've successfully connected to your Asana account, you will see a message `Your Asana account YOUR_ASANA_LOGIN is connected.`

## Configure project-level settings

Asana integration is configured on a per-project basis in Rollbar.

* Click on **Settings** then **Notifications**
* Click on **Asana**.
* Select which authorization token will be used to create and update Asana tasks, as well as the Workspace or Team where the tasks will be located, then click **Save Settings** 
* Specify the rules you'd like to have for automatically creating and updating Asana tasks.  For more details on the available options, see our [Issue Tracking guide](/docs/issue-tracking/#automatic-issue-tracking).
* To ensure that your account is correctly configured, click **Send Test Notification**.  If successful, you'll see a link that allows you to view the test task which was created.
* To activate the Asana integration, set the toggle to **Enabled**.

Your project is now ready to [manually](/docs/issues-tracking/#manual-issue-tracking/) or [automatically](/docs/issue-tracking/#automatic-issue-tracking) create and update Asana tasks.
