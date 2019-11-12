# Installation

1. Navigate to the [Rollbar for Apex Salesforce package installation page](https://docs.rollbar.com/salesforce-apex/install).

2. To the question _What if existing component names conflict with ones in this package?_ answer: _Do not install_.

3. Select the group of users you want to install Rollbar for Apex for. We recommend selecting _Install for All Users_.

4. Click _Install_.

5. Grant access to Rollbar API in a popup window:
    1. Check the _Yes, grant access to these third-party web sites_ checkbox.
    2. Click _Continue_.
  
6. Wait until the package downloads into your organization. You will see the message _Installing and granting access to all Users..._ with a loader. Wait several seconds.

7. Configure Rollbar for Apex
    1. When the download is finished you will be presented with the package's configuration page.
    2. Provide your Rollbar project's _post_server_item_ access token:
    
        `{{ server_access_token }}`
        
    3. Click _Finish_.
  
8. Wait until Rollbar for Apex prepares your organization to use the SDK.

    1. You will see the following final steps being performed:
    
        - _Salesforce Metadata API enabled_
        - _Rollbar API endpoint allowed_
        - _Rollbar ping successful_
        - _Rollbar Email Service set up_
        - _Apex Notifications forwarding set up_
        - _Access Token correct_
        
    2. When the package and your organization is fully configured, all of them should turn green and you will be presented with a _Success_ installation page.
    
    3. The SDK will send a welcome message to your Rollbar project right away. You should be able to find it in your items view in Rollbar.
  
9. You can now use Rollbar for Apex in your organization.

# Send a test message
Sending a message to Rollbar is as simple as:
```
Rollbar.init();

Rollbar.log('info', 'Hello World');
```

You can copy and paste the above Apex code either to your Developer Console and execute it anonymously (`Developer Console` → `Debug` → `Open Execute Anonymous Window`).

Or just start using Rollbar in your Apex classes.

# Configuration
## Changing the access token
If you need to change the access token of your Rollbar project to which your organization is connected, it's as simple as changing the value of a Custom Settings `RollbarSettings__c`.

You can also go back to the Rollbar for Apex installer VisualForce page: `RollbarConfigure`.

# Additional information
* If you are installing the package in a scratch organization, just add path name from the Salesforce package installation link after your scratch org's domain name, i.e.: 

`https://platform-enterprise-7532-dev-ed.lightning.force.com/packaging/installPackage.apexp?p0=04t2E000003sj2F`.
