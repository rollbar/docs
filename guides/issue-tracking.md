---
title: IP History
---

# Connect Rollbar to your Issue Tracker

Rollbar can integrate with [many popular issue trackers](/docs/tools/#issue-tracking) so you can manage Rollbar-detected errors in your existing workflow.

## Issue Tracking Options

When Rollbar is connected to your issue tracker you can _manually_:

* **Create** an issue to track a Rollbar error.
* **Link** a Rollbar error to an existing issue.

Additionally, Rollbar can be configured to _automatically_:

* **Create** an issue for new or frequently-occurring errors.
* **Reopen** a linked issue when a Rollbar error is reactivated or reopened by a user.
* **Resolve** a linked issue when a Rollbar error is resolved.

## Manual Issue Tracking

Screenshots below are for JIRA , but the same features/concepts apply to all issue tracker integrations.
{: .info}

When issue tracking is enabled for a project, users can manually create an issue for a Rollbar error by clicking the `Create` button at the top of the screen.

![](../images/guides/issue-tracking/create_issue.png)

It's also possible to link a Rollbar error to an existing issue.

![](../images/guides/issue-tracking/link_issue.png)

When a Rollbar error is linked to an issue, the `Create` button is replaced with a `View` button that will take you directly to the issue in your tracker.

![](../images/guides/issue-tracking/view_issue.png)

You can change or remove the link via the dropdown menu on the `View` button.

![](../images/guides/issue-tracking/unlink_issue.png)

## Automatic Issue Tracking

Each Rollbar project can be configured to automatically create and update issues in response to triggering events.

To configure the rules for automatic issue tracking, go to **Settings**, then **Notifications** and select your issue tracker.

![](../images/guides/issue-tracking/issues_add_rule.png)

Rules can be filtered to only trigger in specific conditions (e.g. only create issues for items in production that have level error or higher).

![](../images/guides/issue-tracking/issues_edit_rule.png)

## Setup Instructions
* [JIRA](/docs/jira/)
* [Trello](/docs/trello/)
* [GitHub](/docs/github/#github-issues)
* [Bitbucket](/docs/bitbucket/#creating-bitbucket-issues-from-a-rollbar-project)
* [GitLab](/docs/gitlab/#creating-gitlab-issues-from-a-rollbar-project)
* [Asana](/docs/asana)
* [Pivotal](/docs/pivotal)
* [Sprintly](/docs/sprintly)
