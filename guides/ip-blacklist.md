# IP Blacklist

When used in client-side Javascript, Rollbar access tokens are visible to end users and at risk of being used inappropriately to send data to your projects.

Each Rollbar project can be configured with a blacklist of IP addresses from whom we will not accept any data.

To configure the blacklist for your project, go to **Project Settings --> IP Blacklist**, and enter one or more IP addresses, separated by newlines or commas.

*NOTE: Wildcards and ranges are not currently supported for expressing multiple IP addresses.*
