# Integrations Configuration

Certain third-party integrations require your own credentials from the third-party service. You can configure these credentials in `mox.ini`.

## Google OAuth

Create an OAuth app in your Google account, then note its Client ID and Client Secret. Set these as `google.client_id` and `google.client_secret` in `mox.ini`.

## GitHub

Create a GitHub OAuth App in your organization's GitHub account. Set the following configuration settings in GitHub:

- Application name: `rollbar-{yourcompany}`
- Homepage URL: the URL to your Rollbar instance, e.g. `https://rollbar.yourcompany.com`
- Authorization callback URL: the URL to your Rollbar instance, including a trailing slash, e.g. `https://rollbar.yourcompany.com/`

Note the Client ID and Client Secret.

In your `mox.ini`, set the following:

- `github.client_id`: the Client ID
- `github.secret`: the Client Secret
- `github.app_ident`: your application name (if this config entry is not present in your mox.ini, simply add it after `github.secret`)
