Last updated February 3, 2017

Rollbar.com uses the IP addresses listed in outbound_ips.txt to make outbound connections to webhooks, on-premise JIRA and HipChat instances, and so on. If you run such services behind a firewall, you will need to whitelist these IPs so that Rollbar can reach them. Ports 80 and 443 may be used.

The IP addresses listed in api_ips.txt are the IP addresses of the Rollbar API servers. If you need to whitelist what IP addresses your own servers can connect to, add these IP addresses to that whitelist so that you/your servers can connect to the Rollbar API.
