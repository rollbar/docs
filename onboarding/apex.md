# Installation

1. Navigate to the (Rollbar for Apex Salesforce package installation page)[https://login.salesforce.com/packaging/installPackage.apexp?p0=04t2E000003sj20].

2. To the question [i]What if existing component names conflict with ones in this package?[/i] answer: [i]Do not install.[/i]

3. Select the group of users you want to install Rollbar for Apex. We recommend selecting [i]Install for All Users[/i].

4. Click [i]Install[/i].

5. Grant access to Rollbar API in a pop up window:
  1. Check the [i]Yes, grant access to these third-party web sites[/i] checkbox.
  2. Click [i]Continue[/i].
  
6. Wait until the package downloads into your organization. You will see the message [i]Installing and granting access to all Users...[/i] with a loader. Wait several seconds.

7. Configure Rollbar for Apex
  1. When the download is finished you will be presented with the package's configuration page.
  2. Provide your Rollbar project's `post_server_item` access token.
  3. Click [i]Finish[/i].
  
8. Wait until Rollbar for Apex prepares your organization to use the SDK.
  1. You will see the following final steps being performed:
    - Salesforce Metadata API enabled
    - Rollbar API endpoint allowed
    - Rollbar ping successful
    - Rollbar Email Service set up
    - Apex Notifications forwarding set up
    - Access Token correct
  2. When the package and your organization is fully configured, all of them should turn green and you will be presented with a [i]Success[/i] installation page.
  3. The SDK will send a welcome message to your Rollbar project right away.
  
9. You can now use Rollbar for Apex in your organization.

# Send a test message

# Configuration
