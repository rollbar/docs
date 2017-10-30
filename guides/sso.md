# SAML Identity Providers

NOTE: Users must already exist before they can authenticate via a SAML identity provider. User provisioning from SAML identity providers is not currently supported.
{: .warning}

Rollbar account owners can configure a [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) identity provider to authenticate users.  The following SAML providers have been tested and have specific instructions below:

* [G Suite](#g-suite)
* [Okta](#okta)
* [Bitium](#bitium).

[Other SAML-compliant identity providers](#others) may be used, however we don't provide specific instructions for configuring them.

## G Suite

NOTE:  You must be an admin of your Google Apps for Work account to complete the following steps.
{: .info}

**In G Suite:**

* Open your Google admin panel then click the "Apps" tile.
* Click "SAML apps" then "Create New App".
* Click the "+" button on the bottom right to add a new app.
* In the "Enable SSO for SAML Application" modal, click "Setup my own custom app"
* On the next page of the modal, follow "Option 2" and download the application SAML metadata (an XML file).
* Name your app "Rollbar" and optionally give it a description and/or logo
   ([Download Rollbar logo](https://cdn.rollbar.com/assets/rollbar-logo.153796.o.png)) then click "Next".
* On the Service Provider Details Page
   * Fill in "ACS URL" with `https://rollbar.com/{AccountName}/saml/sso/google/` replacing {AccountName} with your account name, which can be found in the URL when you are logged in (`"https://rollbar.com/{AccountName}/..."`)
   * Fill in "Entity ID" with `https://saml.rollbar.com`
   * Choose Basic Information and Primary Email for `Name ID`
   * Choose EMAIL for `Name ID format`
* On the Attribute Mapping page, add a single attribute statement
   * "Email", Basic Information, Primary Email
* Optionally, assign Rollbar to the appropriate users and groups

**In Rollbar:**

* Click on the avatar for your user and go to `{AccountName} Settings -> Security -> Identity Provider`
* Select your identity provider and then enter the XML SAML metadata for the provider and save it.

## Okta

NOTE: You must be an admin of your Okta account to complete the following steps.
{: .info}

**In Okta:**

* In the "Applications" screen, click "Add Application"
* Find the Rollbar app, then click "Add"
* In the "General Settings" screen, enter your account name, which can be found in the URL when you
   are logged in (`"https://rollbar.com/{AccountName}/..."`) then click "Next".
* In the "Sign-On options" screen, click "Identity Provider metadata" to download the XML metadata
   file then click "Next".
* In the "Assign to People" screen, select which users have access to Rollbar then click "Next".

**In Rollbar:**

* Click on the avatar for your user and go to `{AccountName} Settings -> Security -> Identity Provider`
* Select your identity provider and then enter the XML SAML metadata for the provider and save it.

## Bitium

Check out [Configuring SAML for Rollbar](https://support.bitium.com/administration/saml-rollbar/) on the Bitium site for full instructions.

## Others

Setup procedures for other identity providers will vary. Make sure that users' email addresses are being used as the `Name ID` attribute in the SAML metadata.

## Require Log In via your SAML Identity Provider

Once you have successfully saved metadata for your provider, you have the option of requiring non-owners to login via the identity provider whenever they access your account.  

Users who belong to your account may still log in to other accounts using alternate authentication methods (username/email + password, OAuth via Github or Google), but if they attempt to access a URL specific to your account, they will be required to re-authenticate via your identity provider.
