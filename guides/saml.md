---
title: SAML Identity Providers
---

# SAML Identity Providers

You must be an admin of your Identity Provider account to complete the following steps.
{: .warning}

Rollbar users must already exist before they can authenticate via a SAML identity provider. User provisioning from SAML identity providers is not currently supported.
{: .warning}

Rollbar account owners can configure a [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) identity provider to authenticate users.  The following SAML providers have been tested and have specific instructions:

* [G Suite](https://support.google.com/a/answer/7623671)
* [Okta](/docs/okta/)
* [OneLogin](/docs/onelogin/)
* [Azure](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-rollbar-tutorial)
* [Bitium](https://support.bitium.com/administration/saml-rollbar/)

## Other Identity Providers

Rollbar should work with any identity provider that is compliant with the [SAML 2.0](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) standard.  Setup procedures for other identity providers will vary.

The following fields will likely be required by your identity provider:

* `ACS URL`: `https://rollbar.com/{AccountName}/saml/login/other/`. `{AccountName}` is the slug of your account  `https://rollbar.com/{AccountName}`.
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
