# SAML Identity Providers

You must be an admin of your Identity Provider account to complete the following steps.
{: .warning}

Rollbar users must already exist before they can authenticate via a SAML identity provider. User provisioning from SAML identity providers is not currently supported.
{: .warning}

Rollbar account owners can configure a [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) identity provider to authenticate users.  The following SAML providers have been tested and have specific instructions below:

* [G Suite](#g-suite)
* [Okta](#okta)
* [OneLogin](/docs/onelogin/)
* [Azure](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-rollbar-tutorial)
* [Bitium](https://support.bitium.com/administration/saml-rollbar/)
* [Other identity providers](#other-identity-providers)

[Other SAML-compliant identity providers](#others) may be used, however we don't provide specific instructions for configuring them.

## G Suite

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

## Other Identity Providers

Rollbar should work with any identity provider that is compliant with the [SAML 2.0](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) standard.  Setup procedures for other identity providers will vary.

The following fields will likely be required by your identity provider:

* `ACS URL`: `https://rollbar.com/{{AccountName}}/saml/login/other`. `{accountname}` is the slug of your account  `https://rollbar.com/{AccountName}`.
* `Login URL`: Same as ACS URL
* `Entity ID`: `https://saml.rollbar.com`
* `NameID format`: email address

Additionally, Rollbar requires the following:

* An attribute statement of `Email` must be included.
* Response and Assertion should be signed.
* `HTTP-Redirect` and `HTTP-POST` bindings are required. 

## Require Log In via SAML

Once you have successfully saved metadata for your provider, you have the option of requiring non-owners to login via the identity provider whenever they access your account.  

Users who belong to your account may still log in to other accounts using alternate authentication methods (username/email + password, OAuth via Github or Google), but if they attempt to access a URL specific to your account, they will be required to re-authenticate via your identity provider.
