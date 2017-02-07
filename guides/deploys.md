# Deploy Tracking

If you notify Rollbar every time you deploy or release your app, you'll unlock several features that will help your debugging process.

## Deploys

## Suspect Deploy

When deploys are reported to Rollbar, then every detected error will have an entry in its 'Suspect Deploy' tab.

![](../images/guides/deploys/suspect-deploys.png)

The suspect deploy is one of the following:
* The last deploy prior to the first occurrence of the error_(if the item has never been resolved)_.
* The last deploy prior to the reactivation of the error _(if the item was previously resolved)_.
