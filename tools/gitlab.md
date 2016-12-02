## Set up Linking

Each line in your stack trace can be linked to your code in GitLab if it's hosted in a single repository. This has to be done once per project.

1. Go to the Settings section of your project then click on Source Control.
![](../images/tools/gitlab/gitlab1.png)

2. Click on GitLab.
![](../images/tools/gitlab/gitlab2.png)

3. Click Connect to GitLab.
![](../images/tools/gitlab/gitlab3.png)

4. You will be taken to an authorization page in GitLab. Click Authorize.
![](../images/tools/gitlab/gitlab4.png)
![](../images/tools/gitlab/gitlab5.png)

5. Select a repository from the list of available repositories, enter the branch (default is 'master') and a project root within the repository (usually this can be left blank), then save the settings.
![](../images/tools/gitlab/gitlab6.png)

## Viewing GitLab Source Code from Rollbar
Once you've successfully connected to a GitLab repository, Rollbar error tracebacks and deploy reports will include links to specific lines of code and revisions in your repository.
