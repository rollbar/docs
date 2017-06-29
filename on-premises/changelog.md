# Changelog

### 0.7.0

- fixes for multi-host configure.sh bugs
- don't erase old ssl cert files when upgrading
- set beanstalk to persist to disk
- upgrade from sphinx to elasticsearch for search engine
- added options for configuring consul ports and domain name

### 0.6.0

- Fix problem using project api to manage projects.

### 0.5.0

- Fix problem with ProGuard control panel.

- Update nginx configuration to be more compliant with best practices.

### 0.4.0

- Update consul configuration to work across server reboots.

- Pulled in all the latest rollbar code since the last release.

### 0.3.0

- Made enterprise_unlimited the standard pricing plan.

- Pulled in all the latest rollbar code since the last release.

### 0.2.0

- Added ability to ignore projects in new_raw_item_worker to aid in migrating
  data for on-premise customers.

- Pulled in all the latest rollbar code since the last release.

### 0.1.1

- Fixed a bug in the real-time server which was causing the UI to not update in
  real-time.

### 0.1.0

- This is the baseline release of the Rollbar on-premise distribution.
