---
title: Auto-Resolve Items
---

# Auto-Resolve Items

You can configure Rollbar to automatically resolve active items to simplify your error management workflow.  The options are set per environment, and can be found by going to **Settings -> Auto-Resolve** in each of your projects.

## Inactive Items

This option will automatically resolve items if they have not occurred in a certain number of days.  Items are checked for inactivity every 30 minutes and whenever you update your settings.

## On Deploy

This option allows you to resolve all active items whenever you report a [deploy](/docs/deploy-tracking/).
