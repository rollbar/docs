# Connecting JIRA to Rollbar

For general information about Rollbar's issue tracking features, check out the [Issue Tracking guide](../issue-tracking/). 
{: .info}

### In Rollbar

1. Visit the Settings page in Rollbar and go to Notifications. From the Notifications Settings you
   will select JIRA from the list of "Available Channels".
2. Add your JIRA username, password, and server URL, and click 'Enable JIRA integration'.
3. Once you've authorized, you'll be able to customize the type of notifications and frequency you
   want to automatically create Issues on your JIRA Projects.
4. Turn specific Items in Rollbar into Issues in JIRA. When viewing an Item in Rollbar simply click
   the button "Create JIRA Issue" to send the error details to JIRA.
5. You can also link an Item in Rollbar to an existing JIRA Issue. When viewing an Item, select the
   drop down next to the JIRA button and then click "Link existing JIRA Issue" and copy and paste
   the URL for the JIRA Issue you would like to link.

Congratulations! You have now integrated Rollbar with your JIRA account. Events from Rollbar will
automatically create Issues on your JIRA Projects. If you want, you can customize the default rules
by editing, adding, or deleting them.

### View Rollbar info in JIRA
_NOTE: This feature is only available in JIRA Cloud, not in self-hosted JIRA versions_

By adding the [Rollbar for JIRA](https://marketplace.atlassian.com/plugins/com.rollbar.jira/cloud/overview)
add-on to your JIRA Cloud instance, you can view Rollbar error data in the corresponding JIRA issues.

The data appears in the right column in a section entitled 'Rollbar Linked Items' and includes:

* Occurrences and deployments in the past 24 hours
* Error status
* Number of total occurrences
* Number of unique IPs affected
* Datetime first seen
* Datetime last seen

To install the Rollbar for JIRA add-on within your JIRA account:

1. Go to JIRA Administration --> Add-ons
2. Enter "Rollbar" in the search field
3. Click on "Install" on the Rollbar for JIRA add-on

To install Rollbar for JIRA from the Atlassian Marketplace:

1. Go to <https://marketplace.atlassian.com/plugins/com.rollbar.jira/cloud/overview>
2. Click 'Get it Now'

If you've already set up your Rollbar account to create issues in JIRA per the instructions above,
you will automatically start seeing Rollbar Linked Item data in your linked JIRA issues.
