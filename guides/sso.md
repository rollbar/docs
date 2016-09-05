If your Rollbar account is on a [paid plan](https://rollbar.com/pricing/), then you can enable
[SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language)-based single sign-on (SSO)
using [Google Apps for Work](https://apps.google.com/) and/or [Okta](https://www.okta.com/).

NOTE: Users must already exist before they can authenticate via SSO. User provisioning via SSO is
not currently supported.
{: .warning}

### Enabling SSO with Google Apps for Work

NOTE:  You must be an admin of your Google Apps for Work account to complete the following steps.
{: .info}

1. Open your Google admin panel then click the “Apps” tile.
2. Click “SAML apps” then “Create New App”.
3. Click the “+” button on the bottom right to add a new app.
4. In the “Enable SSO for SAML Application” modal, click “Setup my own custom app”
5. On the next page of the modal, follow “Option 2” and download the application SAML metadata (an XML file).
6. Name your app "Rollbar" and optionally give it a description and/or logo
   ([Download Rollbar logo](https://d26gfdfi90p7cf.cloudfront.net/rollbar-logo.153796.o.png)) then click “Next”.
7. On the Service Provider Details Page
  * Fill in “ACS URL” with `https://rollbar.com/{AccountName}/saml/sso/google/` replacing
    {AccountName} with your account name, which can be found in the URL when you are logged in
    (`"https://rollbar.com/{AccountName}/..."`)
  * Fill in "Entity ID" with `https://saml.rollbar.com`
  * Choose Basic Information and Primary Email for `Name ID`
  * Choose EMAIL for `Name ID format`
    ![](https://d26gfdfi90p7cf.cloudfront.net/gapps_service_provider_details.153812.l.png)
8. On the Attribute Mapping page, add a single attribute statement
  * "Email", Basic Information, Primary Email
    ![](https://d26gfdfi90p7cf.cloudfront.net/gapps_attribute_mapping.153798.l.png)
9. Optionally, assign Rollbar to the appropriate users and groups
10. In Rollbar, go to account settings then "SSO".
11. In the text area in the “Add Google as a new SAML Identity Provider” panel, paste of the
    XML contents of the metadata file downloaded from Google apps and click "Save".

### Logging in to Rollbar with a Google Apps account

Once SSO with Google Apps has been successfully configured, there are two ways a user can access
Rollbar using a Google account

Within any Google application, click on the App launcher icon and then select the Rollbar app.

![](https://d26gfdfi90p7cf.cloudfront.net/screen_shot_2016-07-08_at_50539_pm_480.153799.l.png)

When prompted with a Rollbar login page, click on the Google icon

![](https://d26gfdfi90p7cf.cloudfront.net/Screen-Shot-2016-07-14-at-34355-PM.153813.o.png)

### Enabling SSO with Okta

NOTE: You must be an admin of your Okta account to complete the following steps.
{: .info}

1. In the "Applications" screen, click "Add Application"
2. Find the "Rollbar" app, then click "Add"
3. In the "General Settings" screen, enter your account name, which can be found in the URL when you
   are logged in (`"https://rollbar.com/{AccountName}/..."`) then click "Next".
4. In the "Sign-On options" screen, click "Identity Provider metadata" to download the XML metadata
   file then click "Next".
   ![](https://d26gfdfi90p7cf.cloudfront.net/otka_identity_provider_metadata.153800.o.png)
5. In the "Assign to People" screen, select which users have access to Rollbar then click "Next".


### Logging in to Rollbar with Okta

Once SSO with Okta has been successfully configured, users can login via the Okta "My Applications"
screen, a Chrome Plugin, or the Rollbar login page.
