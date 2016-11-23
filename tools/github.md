Rollbar is better with GitHub! Get single-sign on with GitHub, send your rollbar items to GitHub
Issues, link your Rollbar stack traces to the code where it happened, resolve items when a
particular commit is deployed, and show the commits that were included with each deploy.

### Connect your Account

Get started by going to your [account settings](https://www.rollbar.com/settings/integrations).
Navigate to the GitHub tab and click 'Connect with GitHub':

![](../docs/images/tools/github/github1.png)
![](../docs/images/tools/github/github2.png)

This enables single sign on (you can log in with the 'Log in with GitHub' button), and enables the
GitHub integration settings for all your projects.

### Set up Linking

Each line in your stack trace can be linked to your code in GitHub if it's hosted in
a single repository. This has to be done once per project.

#### Link to GitHub

1. Go to the Settings section of your project then click on Source Control. Then click on GitHub.
![](../docs/images/tools/github/github3.png)

2. Click Connect to GitHub. 
![](../docs/images/tools/github/github4.png)
![](../docs/images/tools/github/github5.png)

3. Select a repository from the list of available repositories, enter the branch (default is 'master') and a project root within the repository (usually this can be left blank), then save the settings.
![](../docs/images/tools/github/github6.png)
![](../docs/images/tools/github/github7.png)

#### Configure your notifier

In order to let our servers know that you want it to try linking your stack trace to the files on
GitHub you should send the "server.root" key. A lot of the time that can be "/", to indicate that
all files can be linked to a file in GitHub.

All official Rollbar notifiers can send this key. See the documentation for your notifiers to learn
exactly how.

An additional benefit of correctly setting the server root is that any strings of vendor code in
your stack trace, portions that don't come from a subdirectory of your server root, will be
collapsed. This lets you focus on where your code went wrong. It also improves how Rollbar groups
that error. We strip off the server root from your code where possible before using the filenames as
part of the grouping fingerprint. This means you can host the code from varying locations on your
servers, and still correctly see otherwise identical errors as part of a single group.

Code that is considered in-project because of the 'project_package_paths' key will *not* be linked
to GitHub at this time.

### GitHub Issues

After connecting with GitHub you can integrate GitHub issues to automatically create
issues when Rollbar items arrive, or to add a 'Create GitHub Issue' button to the item page. You
should do this for each project you want integrated with GitHub issues.

To do this navigate to your project notification settings ("Settings" in top navbar then
"Notifications" on the left-hand side navbar). Click the "GitHub Issues" link and fill out the form
to set up your GitHub issues integration.

### Resolving Items

For information on resolving Rollbar items via commit, you can find the
documentation at [Resolving Items via Commits](https://rollbar.com/docs/resolve-via-commits/).
