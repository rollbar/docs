# Invites

These calls require an account-level access token, which should be provided in the query string. The prefix for all URLs is `https://api.rollbar.com`

<!-- Sub:[TOC] -->

## Get an invite

    GET /api/1/invite/:id


## List invites for a team

Returns all invites ever sent for the team--pending, accepted, rejected, and canceled.

    GET /api/1/team/:id/invites


## Invite a user to a team

Invites a user to the specific team, using the user's email address.

If the email address belongs to an existing Rollbar user, they will be immediately added to the team, and sent an email notification. Otherwise, an invite email will be sent, containing a signup link that will allow the recipient to join the specified team.

    POST /api/1/team/:id/invites

### Parameters

Name | Type | Description
-----|------|-------------
`email`|`string`|**Required.** Email address to invite.

Params must be supplied as JSON, and as the body of the request. Be sure to set the header `Content-Type: application/json`.


## Cancel an invite

Cancels an invite, making it no longer valid to accept. If it has already been accepted, use `DELETE /team/:team_id/user/:user_id` instead.

    DELETE /api/1/invite/:id


-----

Last updated: November 26, 2013
