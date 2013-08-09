# How to Integrate Mailgun with Rollbar

You can set up webhooks through Mailgun to report any unsubscribes, spam complaints, bounces, and failures to Rollbar. All that is required is to enter a webhook URL in various areas of the Mailgun control panel for each domain you are interested in keeping track of.

Use the following webhook URL:

<pre>https://rollbar.com/callback/mailgun/POST_SERVER_ITEM_ACCESS_TOKEN?environment=production&level=warning</pre>

- A `post_server_item` access token must be used in the URL.
- The `environment` param is required.
- The `level` param is optional and defaults to `warning`.

### Setup ###

1.  Go to your <a href="https://mailgun.com/cp" target="_blank">Mailgun control panel</a>.
2.  Enter the above webhook URL for the domains and event types you want to observe. For each of the below events, make sure to select the domain you want first in the domain dropdown on the page.
    - For failure reports, find the webhook setting in the <a href="https://mailgun.com/cp/log" target="_blank">Logs</a> tab.
    - For bounce reports, find the webhook setting in the <a href="https://mailgun.com/cp/bounces" target="_blank">Bounces</a> tab.
    - For unsubscribe reports, find the webhook setting in the <a href="https://mailgun.com/cp/unsubscribes" target="_blank">Unsubscribes</a> tab.
    - For complaint reports, find the webhook setting in the <a href="https://mailgun.com/cp/spamreports" target="_blank">Complaints</a> tab.
