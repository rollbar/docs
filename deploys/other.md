# Other platforms

When a deploy has completed successfully, make an HTTP POST to
`https://api.rollbar.com/api/1/deploy/` with the following params:

access\_token
:   Your post\_server\_item project access token. Required.

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
