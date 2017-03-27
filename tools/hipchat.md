# Connect Rollbar to Hipchat

For general information about Rollbar's alerting features, check out the [Notifications guide](../notifications/). 
{: .info}

### Setup

Configuration is per-project in Rollbar.

1.  Head to the Notification settings page for a project: Dashboard -> Settings -> Notifications -> HipChat.
2.  Enter the API Auth Token, Room name or ID, and server URL (if you host HipChat on your own server), and click 'Enable HipChat Integration'.
3.  Congrats! HipChat is now integrated with Rollbar. Default rules will
    have been created for the various events that Rollbar notifies on.
    You can customize the rules by editing them, deleting them, or
    adding new ones.
       
### Tips & Tricks
* You can customize the content of Hipchat messages using [notication variables](/docs/notification-variables/).
