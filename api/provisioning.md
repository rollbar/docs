---
title: API Reference - Provisioning
---

# Provisioning API

You can use this set of API calls to create projects, invite users to join them, and perform a few
basic administration features.

API calls in this section require an access token from your *account*. These tokens can be found in
Account Settings &raquo; Access Tokens.


## Tutorial

In this tutorial, we'll show how to:

- create a project
- invite a user to it, by email address

You'll need your read/write account access token from Account Settings &raquo; Access Tokens.

### Create a Project

To create a project, use the `POST /projects` call.

```bash
ACCESS_TOKEN=WRITE_ACCOUNT_ACCESS_TOKEN
API_BASE='https://api.rollbar.com/api/1'
curl -X POST "$API_BASE/projects?access_token=$ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "Project X"}'
```

This returns your new project. Note the `id`; we'll need it later.

```json
{
  "err": 0,
  "result": {
    "id": 200,
    "account_id": 100,
    "name": "Project X"
  }
}
```

### Create a Team

In Rollbar, users access projects via Teams. To add a user to the project, we'll need to create a
Team, add the team to the project, and the finally invite the user to the team.

To create a team, use the `POST /teams` call.

```bash
ACCESS_TOKEN=WRITE_ACCOUNT_ACCESS_TOKEN
API_BASE='https://api.rollbar.com/api/1'
curl -X POST "$API_BASE/teams?access_token=$ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "Project X Developers", "access_level": "standard"}'
```

This returns the new team. Note the `id`; we'll need it in the next step.

```json
{
  "err": 0,
  "result": {
    "id": 300,
    "account_id": 100,
    "name": "Project X Developers",
    "access_level": "standard"
  }
}
```

### Add the Team to the Project

Next, use `PUT /team/:team_id/project/:project_id` to add the project to the team.

```bash
ACCESS_TOKEN=WRITE_ACCOUNT_ACCESS_TOKEN
API_BASE='https://api.rollbar.com/api/1'
TEAM_ID=300
PROJECT_ID=200
curl -X PUT "$API_BASE/team/$TEAM_ID/project/$PROJECT_ID?access_token=$ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "Project X Developers", "access_level": "standard"}'
```

This returns a the team-project object:

```json
{
  "err": 0,
  "result": {
    "team_id": 300,
    "project_id": 200
  }
}
```

### Invite the User to the Team

We now have a new project and a team that can access it. Let's invite someone to it, by email
address. If they are already a Rollbar user, they'll be added to the team immediately. Otherwise,
they will be added to the team once they accept the invite that was emailed to them.

Use `POST /team/:id/invites`:

```bash
ACCESS_TOKEN=WRITE_ACCOUNT_ACCESS_TOKEN
API_BASE='https://api.rollbar.com/api/1'
TEAM_ID=300
curl -X POST "$API_BASE/team/$TEAM_ID/invites?access_token=$ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"email": "foo@example.com"}'
```

This returns the invite object:

```json
{
  "err": 0,
  "result": {
    "id": 400,
    "from_user_id": 123,
    "team_id": 300,
    "to_email": "foo@example.com",
    "status": "pending",
    "date_created": 1385506327,
    "date_redeemed": null
  }
}
```

## More Resources

That's it for the tutorial, but there's much more you can do with the provisioning API. For more
information, see the following pages:

- [Projects](https://rollbar.com/docs/api/projects/)
- [Teams](https://rollbar.com/docs/api/teams/)
- [Invites](https://rollbar.com/docs/api/invites/)

