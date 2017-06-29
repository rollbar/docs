# Changelog

## 0.8.0

Release date: June 29, 2017

### Application

- [Merging and unmerging](https://rollbar.com/blog/introducing-error-merging-and-unmerging/)
- Refreshed visual design, including [updates to the Items screen](https://rollbar.com/blog/improvements-to-managing-errors-in-rollbar/)
- [Source map troubleshooting tools](https://rollbar.com/blog/javascript-source-map-update/)
- Integrations with [Bitbucket](https://rollbar.com/blog/new-bitbucket-integrations/) and [GitLab](https://rollbar.com/blog/rollbar-integration-for-gitlab/)
- New API calls for managing teams, users, and projects
- Countless small improvements and bug fixes

### Infrastructure

- removed the no-longer-used `moxui` service
- nginx now serves the static site, including the login and signup pages
- pinned Elasticsearch version to 2.4.5

## 0.7.1

- added support for data purging
- added ability to fix failed migrations

## 0.7.0

- fixes for multi-host configure.sh bugs
- don't erase old ssl cert files when upgrading
- set beanstalk to persist to disk
- upgrade from sphinx to elasticsearch for search engine
- added options for configuring consul ports and domain name

## 0.6.0

- Fix problem using project api to manage projects.

## 0.5.0

- Fix problem with ProGuard control panel.

- Update nginx configuration to be more compliant with best practices.

## 0.4.0

- Update consul configuration to work across server reboots.

- Pulled in all the latest rollbar code since the last release.

## 0.3.0

- Made enterprise_unlimited the standard pricing plan.

- Pulled in all the latest rollbar code since the last release.

## 0.2.0

- Added ability to ignore projects in new_raw_item_worker to aid in migrating
  data for on-premise customers.

- Pulled in all the latest rollbar code since the last release.

## 0.1.1

- Fixed a bug in the real-time server which was causing the UI to not update in
  real-time.

## 0.1.0

- This is the baseline release of the Rollbar on-premise distribution.
