# Installation

1. Navigate to the [Rollbar for Apex Salesforce package installation page](https://login.salesforce.com/packaging/installPackage.apexp?p0=04t2E000003sj20).

2. To the question _What if existing component names conflict with ones in this package?_ answer: _Do not install_.

3. Select the group of users you want to install Rollbar for Apex. We recommend selecting _Install for All Users_.

4. Click _Install_.

5. Grant access to Rollbar API in a pop up window:
    1. Check the _Yes, grant access to these third-party web sites_ checkbox.
    2. Click _Continue_.
  
6. Wait until the package downloads into your organization. You will see the message _Installing and granting access to all Users..._ with a loader. Wait several seconds.

7. Configure Rollbar for Apex
    1. When the download is finished you will be presented with the package's configuration page.
    2. Provide your Rollbar project's `post_server_item` access token.
        1. Go to _Settings_ in your Rollbar account.
        2. Click the name of the project you want to connect with your organization.
        3. Navigate to _Project Accesss Tokens_ (it should be default section).
        4. Copy the `post_server_item` access token.
        5. Paste the copied access token in the text input in the package's installer.
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
    3. The SDK will send a welcome message to your Rollbar project right away. You should be able to find in your items view in Rollbar.
  
9. You can now use Rollbar for Apex in your organization.

# Send a test message

# Configuration
