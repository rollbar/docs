# IP Blacklist

When used in client-side Javascript, Rollbar access tokens are visible to end users and at risk of being used inappropriately to send data to your projects.

Each Rollbar project can be configured with a blacklist of IP addresses from whom we will not accept any data.

To configure the blacklist for your project, go to **Project Settings --> IP Blacklist**, and enter one or more IPv4/IPv6 addresses or subnets, separated by newlines or commas.  Examples of valid entries include:
* `192.168.0.1`
* `192.168.0.1/24`
* `2620:0:2d0:200:0:0:0:7/128`

