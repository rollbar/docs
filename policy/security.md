[TOC]

# Discolsure and audit

Data is sent to Rollbar via notifiers that are installed and run on customer machines or embedded in web pages and run on customer's user's browsers. There are open-source notifiers written in popular programming languages and platforms, including [Ruby](https://github.com/rollbar/rollbar-gem), [Python](https://github.com/rollbar/pyrollbar), [Node.js](https://github.com/rollbar/node_rollbar), [JavaScript](https://github.com/rollbar/rollbar.js), [PHP](https://github.com/rollbar/rollbar-php), and [others](https://github.com/rollbar). 

Notifiers are small pieces of code that gather and report data to Rollbar over HTTPS. They do not generate any dynamic code or "monkey-patch" libraries, so you do not need to worry about the interfering with your codebase once installed. Notifiers are also designed to run in an asynchornous manner (where available), and should not have a noticeable impact on performance.

Since all of the notifier code is open-source, the community is able and encouraged to audit the source code. All code is hosted on [Github](http://github.com/).

# Secured content

In order to help us improve Rollbar and user experience, Rollbar may use third-party analytics and customer service tools to better understand user behavior on our site. Any data that Rollbar collects is used solely by Rollbar and is not shared, sold or rented to any third-parties.

Data reported by our notifiers is never shared with any third-party service without the express consent of our users. Rollbar integrates with many tools that provide complementary services. Each of these tools must be configured and enabled by a user before any data will be sent to them.

See our [privacy policy](http://rollbar.com/privacy) for more information.

# Data collection

Our [privacy policy](http://rollbar.com/privacy) details the type of data we collect via our website and notifiers.

All data collected from our notifiers is stored in a raw and aggregated form. Both the aggregated and raw data is available via our website as well as our API. More information about our API can be found [here](http://rollbar.com/docs/api_overview/).

# Data transmission

## HTTPS

All data transmitted to Rollbar from our notifiers is done over SSL by default. Users can choose to configure HTTPS or HTTP in each notifier by providing a configuration option or editing the source code directly. We do not perform host authentication over HTTPS nor do we store any passwords in our notifiers. HTTPS is used solely for communication encryption.

## SSL certificates

Notifiers send data to [https://api.rollbar.com/](https://api.rollbar.com/). We have an extended validation SSL certificate which our API servers use to ensure trusted communication between our customers and Rollbar.

## CORS (Cross-origin resource sharing)
 
Rollbar's API servers are configured to allow [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) requests for API endpoints that are used by our JavaScript notifiers. This enables our customers to send data from their users' browsers to Rollbar for processing. Our CORS enabled endpoints only allow POST requests.

## Serialization formats

Data from our notifiers is either serialized into JSON or multipart-mime format before being sent. Our API servers respond with application/json content-type.  

## Infrastructure

## DNS and load balancers

Rollbar's API and web servers use a cluster of load balancers that are hosted around the globe for fast response times. We use [DynECT Managed DNS](http://dyn.com/dynect-managed-dns) for domain name resolution and failover. DynECT automatically fails over to usable API servers in case of an unexpected error or interruption in service from our API tier.

We have load balancers in the following locations:

- Dallas
- San Hose
- Singapore
- Amsterdam

## Internal network

All data transmitted between Rollbar hosts is done over SoftLayer's internal private network. Our main database cluster is in Dallas with redundant hosts in Seattle and San Jose. The SoftLayer private network is only accessible by machines running within its infrastructure.

## Public network

The only hosts that are accessible from the public internet are our load balancers. The hosts run with strict firewall rules that only allow HTTP and HTTPS traffic (as well as SSH for maintenance and development operations.)

# Proxies

None of the notifiers currently support proxies. Work on this is not yet scheduled. Please contact [support@rollbar.com](mailto:support@rollbar.com) if this would be useful for you.

# Data scrubbing

Data scrubbing is the process of removing sensitive information from the data sent to Rollbar by the notifier. All of the notifiers support data scrubbing. Refer to their individual READMEs on github for information regarding configuration.

## Notifiers

By default, notifiers will attempt to remove request parameters that look like sensitive information.

    e.g. the rollbar-gem notifier scrubs the following request parameters by default

    - passwd
    - password
    - password_confirmation
    - secret
    - confirm_password
    - password_confirmation
    - secret_token

    More info can be found in the [README](https://github.com/rollbar/rollbar-gem/blob/master/README.md#data-sanitization-scrubbing).

## Server-side

Currently we do not support data scrubbing on the server-side. If this is important to you, please email [support@rollbar.com](mailto:support@rollbar.com).

# Hosting and data storage

- We are hosted in Softlayer
  - both physical and cloud servers
  - Dallas, San Jose, etc...
- How we lock down our servers
  - internal network for everything except load balancers
  - firewalls with fail2ban
  - ssh best practices
- Data stored in MySQL clusters
  - nightly backups stored in separate datacenter, (seattle)
  - customer data is not encrypted but is compressed
- Data also stored in Softlayer Object Storage
  - access control via SL
- In-memory storage via memcached cluster on private network
  - unencrypted
- Passwords for Rollbar.com are never stored
  - secure, salted hash with unique nonce per user
- Passwords for 3rd party integrations only stored for ...
  - Use access tokens where available, managed through 3rd party sites

# Data access

- Data accessable to all Rollbar employees
  - confidentiality and IP aggreements
- Customer data access is controlled via team configuration
  - provide an admin and non-admin role
  - teams have access to 1 or more projects
  - Owners team can add/remove users including other owners

# Data retention

- Data retention is based on plan type
  - raw data is deleted from disk in MySQL DB
  - kept in Memcache clusters until purged
  - kept in Softlayer Object Storage for undetermined amount of time
  - no longer available through UI
    - Not implemented fully
- Aggregate data retained indefinite amount of time

# For more help

- Link to more articles
- Support link for inquiries

