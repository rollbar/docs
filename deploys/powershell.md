---
title: Tracking Deploys with Powershell
---

# PowerShell Deploy Integration

Use Invoke-WebRequest to send an HTTP POST:

```
$postParams = @{
    access_token="POST_SERVER_ITEM_ACCESS_TOKEN";
    environment="production";
    revision=$(git log -n 1 --pretty=format:"%H");
    local_username=[Environment]::UserName;
}
Invoke-WebRequest -Uri https://api.rollbar.com/api/1/deploy -Method POST -Body $postParams
```

Place this command in your deploy script so that it runs once the deploy has completed successfully.

If the POST is successful, you will receive a JSON response like: `{"data": {}}`. On the command\
line the output will look like this:

```
StatusCode : 200
StatusDescription : OK
Content : {
"data": {}
}
RawContent : HTTP/1.1 200 OK
Connection: keep-alive
X-Response-Time: 8ms
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
Content-Length: 16
Content-Type: application/json;
charset=utf-8
Date: We...
Forms : {}
Headers : {[Connection, keep-alive],
[X-Response-Time, 8ms],
[X-Frame-Options, SAMEORIGIN],
[X-Content-Type-Options, nosniff]...}
Images : {}
InputFields : {}
Links : {}
ParsedHtml : mshtml.HTMLDocumentClass
RawContentLength : 16
```

If using a version control system other than Git, change the revision= line as appropriate to set the revision ID.

### Parameter Reference

access\_token
:   Your project access token. Required.

environment
:   Name of the environment being deployed, e.g. "production". Required.

revision
:   Revision number/sha being deployed. If using git, use the full sha. Required.

local\_username
:   User who deployed. Optional.

rollbar\_username
:   Rollbar username of the user who deployed. Optional.

comment
:   Deploy comment (e.g. what is being deployed). Optional. Will be rendered as Rollbar-flavored Markdown.
