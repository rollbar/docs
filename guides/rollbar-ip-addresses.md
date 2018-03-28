---
title: Rollbar IP Addresses
---

# Rollbar IP Addresses

_Last changed August 19, 2017_

## Outbound IP Addresses 

Rollbar.com uses the IP addresses listed below to make outbound connections to webhooks, on-premise JIRA and HipChat instances, and so on. If you run such services behind a firewall, you will need to whitelist these IPs so that Rollbar can reach them. Ports 80 and 443 may be used.

```
35.184.69.251
```

## Rollbar API Servers

The IP addresses below are for the Rollbar API tier. If you need to whitelist what IP addresses your own servers can connect to, add these IP addresses to that whitelist so that you/your servers can connect to the Rollbar API.

```
35.201.81.77
```

## Rollbar Web Servers

The IP addresses below are for the Rollbar Web tier. If you need to whitelist what IP addresses your team can use to access the Rollbar web interface, add these IP addresses to that whitelist.

```
35.201.93.97
```
