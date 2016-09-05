Use Curl to send an HTTP POST:

```bash
ACCESS_TOKEN=POST_SERVER_ITEM_ACCESS_TOKEN
ENVIRONMENT=production
LOCAL_USERNAME=`whoami`
REVISION=`git log -n 1 --pretty=format:"%H"`

curl https://api.rollbar.com/api/1/deploy/ \
  -F access_token=$ACCESS_TOKEN \
  -F environment=$ENVIRONMENT \
  -F revision=$REVISION \
  -F local_username=$LOCAL_USERNAME
```

Place this command in your deploy script so that it runs once the deploy
has completed successfully.

If the POST is successful, you will receive a JSON response like:

```json
{"data": {}}
```

If using a version control system other than Git, change the `revision=`
line as appropriate to set the revision ID.

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
