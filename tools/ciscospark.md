## Connecting Rollbar to Cisco Spark

For general information about Rollbar's alerting features, check out the [Notifications guide](../notifications/). 
{: .info}

### Setup

Configuration is per-project in Rollbar.

1.  Head to the Notification settings page for a project: Dashboard ->
    Settings -> Notifications -> Cisco Spark.
2.  Click **Connect with Cisco Spark**.
3.  Select the Cisco account you want to integrate with, and authorize the
    permission request.
4.  Select the room you wish to receive messages for.
5.  Click **Enable Cisco Spark Integration**.
6.  Congrats! Cisco Spark is now integrated with Rollbar. Default rules 
    have been created for the various events that Rollbar notifies on.
    You can customize the rules by editing them, deleting them, or
    adding new ones.

### Tips & Tricks

* You can configure what room you send the notifications to on each individual rule.
* You can customize the content of Cisco Spark messages by using [notification variables](/docs/notification-variables/).
* In addition to notification variables, any data value sent in the JSON payload of an item or occurrence may be used as a variable, including custom data. Examples of usage are `{{"{{body.request.url"}}}}` and `{{"{{body.server.host"}}}}`. If your JSON payload includes the custom values `{{"{{ handler: { key: process-job, id:100"}}}}` then you can use the variables `{{"{{body.handler.key"}}}}` and `{{"{{body.handler.id"}}}}` in your notifications. To view the full set of available values, look at the "Params" values of an occurrence in your project. All params besides the ones listed in the above notification variables *must* be prefaced with "body".
