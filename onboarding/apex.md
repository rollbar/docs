# Installation

1. Navigate to the [Rollbar for Apex Salesforce package installation page](https://docs.rollbar.com/salesforce-apex/install).

2. Select the group of users you want to install Rollbar for Apex for. We recommend selecting _Install for All Users_.

3. Click _Install_.
  
4. Wait until the package downloads into your organization. You will see the message _Installing and granting access to all Users..._ with a loader. This may take 60 seconds or more.

5. Click _Continue Install_ and _Setup Forwarding_ when prompted. Wait for the Rollbar package components to be configured.

6. Configure Rollbar for Apex

    1. When the download is finished you will be presented with the package's configuration page.
    
    2. Provide your Rollbar project's _post_server_item_ access token:
    
        `{{ server_access_token }}`
        
    3. Click _Save and Verify_.
    
7. The SDK will send a welcome message to your Rollbar project right away. You should be able to find it in your items view in Rollbar.
  
8. You can now use Rollbar for Apex in your organization.

# Send a test message
Sending a message to Rollbar is as simple as:
```
rollbar.Rollbar.log('info', 'Hello World');
```

You can copy and paste the above Apex code either to your Developer Console and execute it anonymously (`Developer Console` → `Debug` → `Open Execute Anonymous Window`).

Or just start using Rollbar in your Apex classes.

# Additional information
* If you are installing the package in a scratch organization, just add path name from the Salesforce package installation link after your scratch org's domain name, i.e.: 

`https://platform-enterprise-7532-dev-ed.lightning.force.com/packaging/installPackage.apexp?p0=04t2E000003sj7u`.
