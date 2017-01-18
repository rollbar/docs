## How to Integrate VictorOps with Rollbar

You can turn Rollbar events into Alerts in [VictorOps](https://victorops.com/).

### Connect your Account

Get started by going to your [account settings](https://www.rollbar.com/settings/integrations).
Navigate to the VictorOps tab and click 'Connect with VictorOps':

![](../images/tools/victorops/victorops1.png)
![](../images/tools/victorops/victorops2.png)

### Setup

Configuration is per-project in Rollbar.

1.  Head to the Notification settings page for a project: Dashboard -> Settings -> Notifications -> VictorOps.
    ![](../images/tools/victorops/victorops3.png)

2. 	In VictorOps, go to Settings (or Complete Setup) -> Integrations, and choose Rollbar.
	![](../images/tools/victorops/victorops4.png)

3.	Click "Enable Integration" if it's not already enabled.
	![](../images/tools/victorops/victorops5.png)

4.  Copy the API key from VictorOps. In Rollbar, enter the API and routing keys, and click "Enable VictorOps Integration."
	![](../images/tools/victorops/victorops6.png)

5.  Congrats! You have now integrated Rollbar with your VictorOps
    account. Now, when a new error or higher occurs in Rollbar, it will create an Alert in VictorOps, and
    Alerts in VictorOps will be automatically resolved when they are resolved in Rollbar. If you want, you can customize the default
    rules by editing, adding, or deleting them.

6.	Turn specific Items in Rollbar into Alerts in VictorOps. When viewing an Item in Rollbar simply click
	the button "Create VictorOps Alert" to send the error details to VictorOps.
	![](../images/tools/victorops/victorops7.png)
	![](../images/tools/victorops/victorops8.png)

