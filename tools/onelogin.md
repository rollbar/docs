---
title: Integrate Rollbar with OneLogin
---

# OneLogin

[OneLogin](http://www.onelogin.com) can be used as SAML identity provider for your Rollbar account and can be optionally used to automatically provision users.

## Enable SAML Authentication

_In OneLogin:_

* Go to **Apps->Add Apps**  and find Rollbar
* In the Rollbar Configuration tab, accept the defaults (make sure that `SAML 2.0 - user provisioning` is selected) and click **Save**.
* Go to the **Configuration** tab again, and enter your Rollbar account name in the Applications Details section and click **Save**.
* Click **More Actions** -> **SAML Metadata**, download the metadata file, and copy the XML contents.


_In Rollbar:_

* Go to **{Accountname} Settings -> Security -> Identity Provider**.
* Select OneLogin as the identity provider, paste the metadata and click **Save**.
* Optionally select to require users to login via OneLogin.

_In OneLogin:_

* Assign all users who should get access to your Rollbar account to the Rollbar app.

Unless user provisioning has been enabled for your Rollbar account, anyone who accesses Rollbar via OneLogin will need to be invited to Rollbar.  To enable provisioning in your Rollbar account, please contact us via <a href="mailto:sales@rollbar.com">sales@rollbar.com</a>.
{: .info}

## Enable Provisioning

If user provisioning is enabled for your Rollbar account, then users who are added to the Rollbar app in OneLogin will be provisioned in Rollbar.

_In Rollbar:_

* Go to **{Accountname} Settings->Security->Identity Provider**.  If your SAML metadata has been properly configured and your account has provisioning enabled, then a section titled **Provisioning Options** will appear on the page.
* Copy the access token, click **Enable user and team provisioning**, then click **Save**.

_In OneLogin:_

* Go to **Apps->Company Apps** and select Rollbar.
* Go to the **Configuration** tab, and enter the Rollbar access token in the **SCIM Bearer Token** field, then click **Enable**.
* Go to the **Provisioning** tab and do the following:
  * Check **Enable Provisioning for Rollbar**
  * Uncheck all options in **Require admin approval before this action is performed in Rollbar**
  * Select **Delete** as the action to take when a user is deleted in OneLogin.
* Click **Save**.
* Assign users to the Rollbar app, either directly or via a Role.  If the person does not yet have a Rollbar user with the same email address, then choose to provision the user.  The system should display a `provisioned` label next to the user after a few moments.
