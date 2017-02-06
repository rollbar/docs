# Rollbar IP Addresses

_Last updated February 3, 2017_

## Outbound IP Addresses 

Rollbar.com uses the IP addresses listed below to make outbound connections to webhooks, on-premise JIRA and HipChat instances, and so on. If you run such services behind a firewall, you will need to whitelist these IPs so that Rollbar can reach them. Ports 80 and 443 may be used.

```
50.23.219.116
50.23.231.132
75.126.169.212
75.126.169.213
75.126.169.214
75.126.169.215
75.126.169.216
75.126.169.217
75.126.169.221
75.126.67.76
108.168.203.181
184.173.71.211
184.173.71.217
192.155.197.228
192.155.197.238
```

## Rollbar API Servers

The IP addresses below are for the Rollbar API servers. If you need to whitelist what IP addresses your own servers can connect to, add these IP addresses to that whitelist so that you/your servers can connect to the Rollbar API.

```
37.58.71.74
50.97.241.205
75.126.67.75
108.168.203.178
119.81.30.98
169.45.20.48
192.155.197.230
192.155.197.237
198.23.74.38
```
