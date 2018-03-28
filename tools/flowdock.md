---
title: Flowdock Integration
---

# Connect Rollbar to Flowdock

For general information about Rollbar's alerting features, check out the [Notifications guide](../notifications/). 
{: .info}

### In Flowdock

1.  Visit the [API Tokens](https://www.flowdock.com/account/tokens) page
    in Flowdock, and note the token for the flow where you want to
    receive Rollbar notifications.

### In Rollbar

1.  Navigate to the Dashboard of the project you want to integrate with
    Flowdock
2.  Click Settings --> Notifications --> Flowdock
3.  Copy-paste the API Token from Flowdock into the box in Rollbar.
4.  Press Enable Flowdock Integration.
5.  Congrats! You have now integrated Rollbar with your Flowdock
    account. Events from Rollbar will automatically be pushed into your
    flow. If you want, you can customize the default rules by editing,
    adding, or deleting them.

### Tips & Tricks
* You can customize the content of Flowdock messages using [notification variables](/docs/notification-variables/).
