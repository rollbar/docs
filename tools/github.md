---
title: GitHub Integration
---

# Connect Rollbar to GitHub

Rollbar is better with GitHub! Get single-sign on with GitHub, send your rollbar items to GitHub
Issues, link your Rollbar stack traces to the code where it happened, resolve items when a
particular commit is deployed, and show the commits that were included with each deploy.

### Connect your Account

Get started by going to your [account settings](https://www.rollbar.com/settings/integrations).
Navigate to the GitHub tab and click 'Connect with GitHub'.

This enables single sign on (you can log in with the 'Log in with GitHub' button), and enables the
GitHub integration settings for all your projects.

### Set up Linking

For general information about Rollbar's Git integration, check out the [Source Control guide](../source-control/). 
{: .info}

Each line in your stack trace can be linked to your code in GitHub if it's hosted in
a single repository. This has to be done once per project.

#### Link to GitHub

1. Go to the Settings section of your project then click on Source Control. Then click on GitHub.
2. Click Connect to GitHub. 
3. Select a repository from the list of available repositories, enter the branch (default is 'master') and a project root within the repository (usually this can be left blank - [click here](../source-control#serverroot) for more details), then save the settings.
4. Ensure you are sending the `server.root` key with your items. See [here](../source-control#serverroot) for more information.

### GitHub Issues

For general information about Rollbar's issue tracking features, check out the [Issue Tracking guide](../issue-tracking/). 
{: .info}

After connecting with GitHub you can integrate GitHub issues to automatically create
issues when Rollbar items arrive, or to add a 'Create GitHub Issue' button to the item page. You
should do this for each project you want integrated with GitHub issues.

To do this navigate to your project notification settings ("Settings" in top navbar then
"Notifications" on the left-hand side navbar). Click the "GitHub Issues" link and fill out the form
to set up your GitHub issues integration.

### Resolving Items

For information on resolving Rollbar items via commit, you can find the
documentation at [Resolving Items via Commits](https://rollbar.com/docs/resolve-via-commits/).
