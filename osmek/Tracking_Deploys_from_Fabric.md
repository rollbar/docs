<span class="date">05/20/14 at 03:59 PM</span>

Here's an example Fabric command. Call this from your `deploy` command
when a deploy has completed successfully.

``` {data-language="python"}
import requests
def rollbar_record_deploy():
    access_token = 'POST_SERVER_ITEM_ACCESS_TOKEN'
    environment = 'production'
    local_username = local('whoami', capture=True)
    # fetch last committed revision in the locally-checked out branch
    revision = local('git log -n 1 --pretty=format:"%H"', capture=True)

    resp = requests.post('https://api.rollbar.com/api/1/deploy/', {
        'access_token': access_token,
        'environment': environment,
        'local_username': local_username,
        'revision': revision
    }, timeout=3)

    if resp.status_code == 200:
        print "Deploy recorded successfully."
    else:
        print "Error recording deploy:", resp.text
```

### Parameter Reference

access\_token
:   Your project access token. Required.

environment
:   Name of the environment being deployed, e.g. "production". Required.

revision
:   Revision number/sha being deployed. If using git, use the full sha.
    Required.

local\_username
:   User who deployed. Optional.

rollbar\_username
:   Rollbar username of the user who deployed. Optional.

comment
:   Deploy comment (e.g. what is being deployed). Optional.


