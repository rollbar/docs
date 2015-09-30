<span class="date">05/15/14 at 03:29 PM</span>

How to Integrate PagerDuty with Rollbar
=======================================

Rollbar can create, update, and resolve Incidents
in [PagerDuty](http://pagerduty.com/).

In PagerDuty:
-------------

1.  From the PagerDuty dashboard, click Services from the navigation bar
    at the top of the page.

    ![](http://photos.osmek.com/pagerduty_1.133232.o.png)

2.  On the right side of the page, click the green Add New
    Service button.

    ![](http://photos.osmek.com/pagerduty_2.133233.o.png)

3.  Fill in the service name (e.g. "Rollbar").

    ![](http://photos.osmek.com/pagerduty_3.133234.o.png)

4.  Select an escalation policy.

5.  Under Service Type, choose Generic API system.

6.  Click the \*Add Service button at the bottom.

7.  On the service page under Integration Settings, note the string next
    to Service API key.

    ![](http://photos.osmek.com/pagerduty_4.133235.o.png)

In Rollbar:
-----------

1.  Navigate to the Dashboard of the project you want to integrate with
    PagerDuty

    ![](http://photos.osmek.com/pagerduty_5.133222.o.png)

2.  Click Settings

    ![](http://photos.osmek.com/pagerduty_6.133223.o.png)

3.  Click Notifications

    ![](http://photos.osmek.com/pagerduty_7.133224.o.png)

4.  Click PagerDuty

    ![](http://photos.osmek.com/pagerduty_8.133236.o.png)

5.  Copy-paste the Service API key from PagerDuty into the box in
    Rollbar.

    ![](http://photos.osmek.com/pagerduty_9.133237.o.png)

6.  Press Enable PagerDuty Integration.

7.  Congrats! You have now integrated Rollbar with your PagerDuty
    account. Now, when a new error or higher occurs in your production
    environment in Rollbar, it will create an incident in PagerDuty, and
    incidents in PagerDuty will be automatically resolved when they are
    resolved in Rollbar. If you want, you can customize the default
    rules by editing, adding, or deleting them.

    ![](http://photos.osmek.com/pagerduty_10.133238.o.png)


