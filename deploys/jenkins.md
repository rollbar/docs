---
title: Tracking Deploys with Jenkins
---

# Jenkins Deploy Integration

Tracking deployments in Jenkins will allow you to see new errors for each deployment, determine the deployment that is suspected to have caused each error, and automatically resolve errors that were fixed in each deployment. You can read more examples in our blog [Continuous Delivery with Jenkins and Rollbar](/blog/continuous-delivery-with-jenkins/).

To configure Jenkins, use the curl command to notify Rollbar of the deployment:

```bash
curl https://api.rollbar.com/api/1/deploy/ \
  -F access_token=access_token \
  -F environment=development \
  -F revision=${GIT_COMMIT} \
  -F rollbar_username=rollbar_username \
  -F local_username=jenkins_user \
  -F comment='any comments'
```

Place this command in your deploy script so that it runs once the deploy has completed successfully. If successful, Rollbar's API will give a JSON response like this:

```json
{ "data": {} }
```

Replace each of the example values according to the parameter reference below. If using a version control system other than Git, change the `revision=` line as appropriate to set the revision ID.

### Parameter Reference

access\_token
:   Your project access token. Required.

environment
:   Name of the environment being deployed, e.g. "production". Required.

revision
:   The deployment artifact version (Required). Here the Jenkins environment variable GIT_COMMIT is used which will automatically populates the git commit sha. If using git, use the full sha. This can be any version number like BUILD_NUMBER or project maven pom version number. Required.

local\_username
:   User who deployed. Optional. (Ex: jenkins_user).

rollbar\_username
:   Rollbar username of the user who deployed. Optional.

comment
:   Deploy comment (e.g. what is being deployed). Optional.
