# SAML Identity Providers

Users must already exist before they can authenticate via a SAML identity provider. User provisioning from SAML identity providers is not currently supported.
{: .warning}

Rollbar account owners can configure a [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) identity provider to authenticate users.  The following SAML providers have been tested and have specific instructions below:

* [G Suite](#g-suite)
* [Okta](#okta)
* [OneLogin](#one-login)
* [Azure](#azure)
* [Bitium](#bitium)

[Other SAML-compliant identity providers](#others) may be used, however we don't provide specific instructions for configuring them.

## G Suite

You must be an admin of your Google Apps for Work account to complete the following steps.
{: .info}

**In G Suite:**

* Open your Google admin panel then click the **Apps** tile.
* Click **SAML apps** then **Create New App**.
* Click the **+** button on the bottom right to add a new app.
* In the **Enable SSO for SAML Application** modal, click **Setup my own custom app**
* On the next page of the modal, follow **Option 2** and download the application SAML metadata (an XML file).
* Name your app `Rollbar` and optionally give it a description and/or logo (available at https://rollbar.com/media/)  then click **Next**.
* On the Service Provider Details Page enter the following:
   * _ACS URL_: `https://rollbar.com/{AccountName}/saml/sso/google/` replacing {AccountName} with your account name, which can be found in the URL when you are logged in (`"https://rollbar.com/{AccountName}/..."`)
   _Entity ID_: `https://saml.rollbar.com`
   * Choose Basic Information and Primary Email for `Name ID`
   * Choose EMAIL for `Name ID format`
* On the Attribute Mapping page, add a single attribute statement
   * "Email", Basic Information, Primary Email
* Optionally, assign Rollbar to the appropriate users and groups

**In Rollbar:**

* Click on the avatar for your user and go to **{AccountName} Settings -> Security -> Identity Provider**
* Select `Google` as your identity prvider and then enter the XML SAML metadata for the provider and save it.

## Okta

You must be an admin of your Okta account to complete the following steps.
{: .info}

**In Okta:**

* In the **Applications** screen, click **Add Application**.
* Find the Rollbar app, then click **Add**
* In the **General Settings** screen, enter your account name, which can be found in the URL when you are logged in (`"https://rollbar.com/{AccountName}/..."`) then click **Next**.
* In the **Sign-On options** screen, click **Identity Provider metadata** to download the XML metadata file.
* In the **Credential Details** section, make sure that `Application username format` is set to `Email` then click **Done**.
* Assign the appropriate users and groups to Rollbar.

**In Rollbar:**

* Click on the avatar for your user and go to **{AccountName} Settings -> Security -> Identity Provider**
* Select `Okta` as your identity prvider and then enter the XML SAML metadata for the provider and save it.

## OneLogin

**In OneLogin:**

* Go to **Apps -> Company Apps** then click **Add Apps**
* Select the app **SAML Test Connector (IdP w/attr)**
* In the configuration tab, enter `Rollbar` as the display name.  Optionally, you can use icons available at https://rollbar.com/media/ for the app.  Click **Save**.
* Go to the **Configuration** tab, enter the following values, and click **Save**:
  * Audience: `https://saml.rollbar.com`
  * Recipient: `https://rollbar.com/{accountname}/saml/sso/onelogin/` where `{accountname}` is the name found in the URL of your account, e.g. `https://rollbar.com/{accountname}`
  * ACS (Consumer) URL Validator: `.*`
  * ACS (Consumer) URL: `https://rollbar.com/{accountname}/saml/sso/onelogin/` (same value as Recipient field)
* Go to **More Action -> SAML Metadata** to download an XML file containing your SAML metadata  

**In Rollbar:**

* Click on the avatar for your user and go to **{AccountName} Settings -> Security -> Identity Provider**
* Select `OneLogin` as your identity prvider and then paste the XML SAML metadata for the provider and save it.

## Azure

You must be an admin of your Azure account to complete the following steps.
{: .info}

**In Azure**

* Go to **Azure Active Directory** then click **App registrations** and select **New application registration**.
* Enter the following information in the form and save it.
   * Name: `Rollbar`
   * Application type: `Web App / API`
   * Sign-on URL: `https://rollbar.com/{AccountName}/saml/login/azure`. `{accountname}` is the slug of your account  `https://rollbar.com/{AccountName}`.
* Open the app configuration, select **Properties** and set the following value:
   * App ID URI: `https://saml.rollbar.com`
* Go to **Endpoints**, then open **Federation Metadata Document** and copy the XML metadata.

**In Rollbar:**

* Click on the avatar for your user and go to **{AccountName} Settings -> Security -> Identity Provider**
* Select `Azure` as your identity provider and then paste the XML SAML metadata for the provider and save it.


## Bitium

Check out [Configuring SAML for Rollbar](https://support.bitium.com/administration/saml-rollbar/) on the Bitium site for full instructions.

## Others

Setup procedures for other identity providers will vary. Make sure that users' email addresses are being used as the `Name ID` attribute in the SAML metadata.

The following fields will likely be required by your identity provider:
* `ACS URL`: `https://rollbar.com/{{AccountName}}/saml/login/other`. `{{accountname}}` is the slug of your account  `https://rollbar.com/{AccountName}`.
* `Entity ID`: `https://saml.rollbar.com`

## Require Log In via SAML

Once you have successfully saved metadata for your provider, you have the option of requiring non-owners to login via the identity provider whenever they access your account.  

Users who belong to your account may still log in to other accounts using alternate authentication methods (username/email + password, OAuth via Github or Google), but if they attempt to access a URL specific to your account, they will be required to re-authenticate via your identity provider.
