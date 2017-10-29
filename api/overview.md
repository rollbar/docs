Overview
--------

The Rollbar API provides a RESTful interface to much of the data in the
system. It is used by our official libraries to report exceptions,
deploys, and other messages. It can be used to create notifiers for
additional languages, get data out to integrate with other systems, or
whatever else you can imagine. If the API is missing something you'd
like to see, please [let us know](mailto:support@rollbar.com).

At this time the best way to discover the available resources/calls is
by exploring the [test console](https://rollbar.com/docs/test_console/).

### Ping

To test whether you're able to ping the API server, you can simply run the following command:

```bash
curl 'https://api.rollbar.com/api/1/status/ping'
```

You will get back `pong` from our server if your request was successful.

### Timestamps

All timestamps (inputs and outputs) are GMT unix timestamps.

### Authentication

Authentication is done via access token included as a parameter. For GET
requests, it should be included as a query parameter:

```bash
curl 'https://api.rollbar.com/api/1/item/12345?access_token=YOUR_ACCESS_TOKEN'
```

All access tokens are project-specific and only provide access to the
project they are assocaited with. You can find and administer your
access tokens in Settings»Access Tokens. Access tokens can have any or
all of the following scopes:

post\_server\_item
:   Can perform all POST requests

post\_client\_item
:   Can perform POST requests to /deploy/ and /item/, but only if the
    item has a client-side platform.

read
:   Can perform all GET requests

write
:   Can perform PATCH requests to change item statuses.

New projects are created with four tokens, one with each scope. As
client tokens often need to be embedded in publicly-visible code (i.e
the HTML source of a page), we recommend keeping this setup with an
isolated post\_client\_item-only token.

### Error responses

The API can return the following error codes:

|---
| Code | Type | Description
|-|-|-
| 400 | Bad request | The request was malformed and could not be parsed.
| 403 | Access denied | Access token was missing, invalid, or does not have the necessary permissions.
| 404 | Not found | The requested resource was not found. This response will be returned if the URL is entirely invalid (i.e. `/asdf`), or if it is a URL that could be valid but is referencing something that does not exist (i.e. `/item/12345`).
| 413 | Request entity too large | The request exceeded the maximum size of 128KB.
| 422 | Unprocessable Entity | The request was parseable (i.e. valid JSON), but some parameters were missing or otherwise invalid.
| 429 | Too Many Requests | If rate limiting is enabled for your access token, this return code signifies that the rate limit has been reached and the item was not processed.

### Examples

Link | Author | Language | Description
-----|--------|----------|------------
[api-examples](https://github.com/rollbar/api-examples)|Rollbar|Python|Examples using RQL, deploys, occurrences, and reports
[api-people-example](https://github.com/rollbar/api-people-example)|Rollbar|Python|Shows how to gather the Person data for each occurrence of a list of items
[rolltools](https://github.com/jslate/rolltools)|[Jonathan Slate](https://github.com/jslate)|Ruby|A few utilities using the Rollbar API

-----
Last updated: August 27, 2017
