# OneLogin

# Connecting Rollbar to OneLogin

_In OneLogin:_

* Go to **Apps->Add Apps**  and find Rollbar
* In the Rollbar Configuration tab, accept the defaults (make sure that `SAML 2.0 - user provisioning` is selected) and click Save.
* Go to the **Configuration** tab again, and enter your Rollbar account name in the Applications Details section and click Save.
* Click **More Actions** -> **SAML Metadata**, download the metadata file, and copy the XML contents.


_In Rollbar:_

* Go to {Accountname} Settings -> Security -> Identity Provider.
* Select OneLogin as the identity provider, paste the metadata and click Save.
* Optionally select to require users to login via OneLogin.

_In OneLogin:_

* Assign all users who should get access to your Rollbar account to the Rollbar app.

Unless user provisioning has been enabled for your Rollbar account, anyone who accesses Rollbar via OneLogin will need to be invited to Rollbar.  To enable provisioning in your Rollbar account, please contact us via <a href="mailto:support@rollbar.com">support@rollbar.com</a>.
{: .info}
