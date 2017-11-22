# Changelog

## 0.8.4

Release date: November 21, 2017

### Application

- New feature: ability to restrict authentication to SAML-only. [More info](https://changelog.rollbar.com/require-saml-authentication-38730)
- New feature: system-controlled "default rate limits". Admins can configure the system default and also override on a per-token basis using the newly-accessible administrator view. When a user-controlled limit is also defined (via the normal non-admin view), both limits are in effect. [More info](https://changelog.rollbar.com/default-rate-limits-on-project-access-tokens-37808)
- New feature: ability to edit or merge all items matching a search in a single action. [More info](https://changelog.rollbar.com/edit-merge-all-items-at-once-34467)
- Fix: test emails are now sent only to the user who clicks "Send test notification", rather than to all users who can access the project.
- Fix: CSV downloads now work correctly. To apply this fix to an existing installation, edit your `mox.ini` config file (most likely located in `/etc/rollbar/mox.ini`) as follows: 

  ```diff
  --- a/standalone.ini
  +++ b/standalone.ini
  @@ -55,8 +55,8 @@ pyramid.debug_routematch = false
   pyramid.debug_templates = false
   pyramid.default_locale_name = en
   pyramid.includes =
  +    pyramid_tablib
       rollbar.contrib.pyramid
  -    pyramid_tm
   ```

### Infrastructure

- Added external link for `web` container to `haproxy:redis`. NOTE: if upgrading from an existing version, apply the following change to your `mox.ini` config file:

  ```diff
  --- a/standalone.ini
  +++ b/standalone.ini
  @@ -84,6 +84,9 @@ mako.output_encoding = utf-8
   memcache.default.server_list = memcache:11211/1
   memcache.raw.server_list = memcache:11211/1
   
  +redis.host = redis
  +redis.port = 6379
  +
   beanstalk.host = beanstalk
   beanstalk.port = 11300
  ```
- New container: autoresolve_old_items_periodic
- Removed container: project_processing_etl

## 0.8.3

Release date: September 11, 2017

### Application

- New feature: JavaScript Telemetry. Requires upgrading to rollbar.js 2.2.4 or higher. [More info](https://rollbar.com/docs/telemetry/)
- New feature: Google OAuth authentication
- Improvements to [JIRA integration](https://changelog.rollbar.com/jira-updates-oauth-more-29665)
- Various bug fixes and UI polish

## 0.8.2

Release date: July 18, 2017

### Application

- Improvement: method names now unminified when source maps are applied. [More info](https://changelog.rollbar.com/de-minify-js-method-names-27541)
- Improved frontend page load time and rendering performance
- Various bug fixes and polish

### Infrastructure

- New worker type: project_task_worker

## 0.8.1

Release date: June 30, 2017

### Application

- Fixed an issue causing flashes of unrendered content on some page loads

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
