# How to Integrate Flowdock with Rollbar

Rollbar can send messages about exceptions or deploys to your flow in [Flowdock](http://flowdock.com).

## In Flowdock

1. Visit the [API Tokens](https://www.flowdock.com/account/tokens) page in Flowdock, and note the token for the flow where you want to receive Rollbar notifications.
    
    <img src="/static/img/docs/flowdock_1.png">

## In Rollbar

1. Navigate to the Dashboard of the project you want to integrate with PagerDuty
    
    <img src="/static/img/docs/pagerduty_5.png">
    
2. Click **Settings**

    <img src="/static/img/docs/pagerduty_6.png">

3. Click **Notifications**
    
    <img src="/static/img/docs/pagerduty_7.png">

4. Click **Flowdock**

    <img src="/static/img/docs/flowdock_2.png">

5. Copy-paste the API Token from Flowdock into the box in Rollbar.
    
    <img src="/static/img/docs/flowdock_3.png">

6. Press **Enable Flowdock Integration**.

7. Congrats! You have now integrated Rollbar with your Flowdock account. Events from Rollbar will automatically be pushed into your flow. If you want, you can customize the default rules by editing, adding, or deleting them.
    
    <img src="/static/img/docs/flowdock_4.png">

