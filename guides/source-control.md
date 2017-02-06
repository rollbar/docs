# Integrating Rollbar with Source Control

Rollbar can be integrated with your [Github](../github/), [Bitbucket](../bitbucket/), or [Gitlab](../gitlab/) repository.  When Rollbar is connected to your source control system, new debugging features are unlocked.

## View source from stack traces

When a Rollbar project is connected to a git repository, stack traces will include links to each file in the code version where the error was most recently activated.

![Linking from stack trace to source code](https://rollbar.com/assets/homepage/images/integrations/stacktrace-bitbucket-linked.png)

## View commits in each deploy
When a Rollbar project is connected to a git repository, the list of commits included in each deploy will include URLs so you can view the diff for each commit as well as the entire deployed code version.

![Deploy with links to commits](../images/guides/source-control/deploy-source-links.png)

## View undeployed commits
When a Rollbar project is connected to a git repository, any commit that has been merged to your master branch but not yet deployed will be highlighted at the top of the Deploys screen.

![Undeployed commits](../images/guides/source-control/undeployed_changes.png)

## Resolve via commits
By adding an appropriately formatted message when committing a code change, you can tell Rollbar to automatically mark an item as resolved as soon as the commit is deployed to production.

```
$ git commit -m 'resolves rb#12345'
```
To learn more, check out [Resolving Items via commit](..//resolve-via-commits/)

## Setup Instructions
To connect a Rollbar project to your git repository, just follow the steps on one of the following pages.

* [Github](../github/)
* [Bitbucket](../bitbucket/)
* [Gitlab](../gitlab/)
