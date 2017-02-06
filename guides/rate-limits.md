# Rate Limits

Rate limits allow you to control how many occurrences are saved and
processed. In turn, this gives you control over how many occurrences
count towards your monthly bill.

Each project access token can be individually configured with a
different rate limit. Once the limit is reached, all calls to POST items
will return HTTP status code `429 Too Many Requests` until the next rate
limit window begins.

If you go over your rate limit, a new error will be generated in your
project: it will show up on your dashboard, on your API errors page, and
(depending on your notification settings) you will receive an email. You
can then resolve, comment and configure notification settings for the
generated error the same way you would for others. Note: these errors
are not counted towards your bill.

You can change your rate limits as often as you want.

### Configuration

Starting from a project, Go to Settings -> Project Access Tokens and
click on the

<button class="btn btn-sm" style="padding: 5px 10px;"><span class="glyphicon glyphicon-pencil"></span></button>

button next to the access token to configure.

Next, choose a time window from the rate limit dropdown menu. Choices
are:

1.  No Limit
2.  1 minute
3.  5 minutes
4.  30 minutes
5.  1 hour
6.  1 day
7.  1 week
8.  30 days

Finally, enter in the maximum number of items to be saved and processed
in the text box to the left of the dropdown menu and click the

<button class="btn btn-sm" style="padding: 5px 10px;"><span class="glyphicon glyphicon-ok"></span></button>

button to save.

e.g. 100 in 5 minutes

**Note:** New rate limits and changes to existing limits will take effect immediately.
{: .warning}

Details
-------

### Response Codes

If your access token has a rate limit and has reached
it, all successful API calls will result in an HTTP 429 (Too Many
Requests) response code. Once the limit is reached, there can be a short
delay before our servers begin to reply with a 429. This does not mean
that these items will count towards your bill. These items will not be
processed and will not appear on your dashboard.

**Important!** If you're using a custom script or library to POST items you should make sure it can
handle the 429 response code.
{: .error}

### Billing

At the end of your billing cycle, the total charge is calculated based
on all items saved and processed. This will not include items that were not processed due to your
rate limits.
