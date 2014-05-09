# Sending Logentries alerts to Rollbar

If you use [Logentries](https://logentries.com), you can set up alerts to report to Rollbar. For example, you can create an tag matching `error`, and then configure Logentries to notify Rollbar whenever an event in Logentries matches.

A "message"-type Item will appear in Rollbar, using the log message from Logentries that triggered the alert. The host, timestamp, and context lines will be included as well.

Use the following webhook URL:

<pre>https://api.rollbar.com/api/1/webhook/logentries?access_token=POST_SERVER_ITEM_ACCESS_TOKEN&environment=production</pre>

- A `post_server_item` project access token must be used in the URL.
- The `environment` param is required.

### Setup

1. In Logentries, click "Tags & Alerts" in the top nav
2. Click "Create Tag / Alert", or modify an existing one
3. Configure the tag. Then press "Add Alert" near the bottom
4. Check the "Web hook" box, and enter the webhook url from above.
5. Save the tag/alert.

