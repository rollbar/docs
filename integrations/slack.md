# How to Integrate Slack with Rollbar

Rollbar can send messages about exceptions and deploys to a channel or group in [Slack](https://slack.com).

### Setup ###

Configuration is per-project in Rollbar. 

1. Head to the Notification settings page for a project: Dashboard -> Settings -> Notifications -> Slack.

2. Click **Connect with Slack**

3. Select the Slack team you want to integrate with, and authorize the permission request.

4. Select the channel or group you wish to receive messages for

5. Click **Enable Slack Integration**

6. Congrats! Slack is now integrated with Rollbar. Default rules will have been created for the various events that Rollbar notifies on. You can customize the rules by editing them, deleting them, or adding new ones

