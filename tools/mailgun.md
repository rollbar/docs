---
title: Mailgun Integration
---

## Sending Mailgun Events to Rollbar

You can set up webhooks through Mailgun to report any unsubscribes, spam
complaints, bounces, and failures to Rollbar. All that is required is to
enter a webhook URL in various areas of the Mailgun control panel for
each domain you are interested in keeping track of.

Use the following webhook URL:

    https://rollbar.com/callback/mailgun/ACCESS_TOKEN?environment=production&level=warning

### URL Parameters

-   Replace ACCESS\_TOKEN with a `post_server_item` access token for the
    project where events should be sent.
-   The `environment` param is required. Events will be reported into
    this environment in Rollbar.
-   The `level` param is optional and defaults to `warning`.

### Setup

1.  Go to your [Mailgun webhooks settings](https://mailgun.com/cp).
2.  Choose a domain using the dropdown on the left.
3.  Enter the above webhook URL for the each event type you want to
    observe.
4.  Repeat for other domains as desired.
