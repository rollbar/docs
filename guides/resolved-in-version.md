You can track which versions or revisions your errors are resolved in. When resolving items within Rollbar, you have the option of entering a revision or version number. If one is entered, it will appear in the item’s status history to let anyone looking at the item better understand specifically when it was fixed.

This version can be combined with a new code_version parameter set in the configuration options of the latest versions of our notifiers. This can be set to either a numerical value (eg. 1, 24, 300), a semantic version value (eg. 1.0.3, 2.9), or a Git revision SHA. Here are examples on how to set this parameter in our JavaScript and Ruby notifiers:

In the JavaScript snippet:

```
var _rollbarConfig = {
    # ... other configuration
    payload: {
        environment: "production",
        version: "3da541559918a808c2402bba5012f6c60b27661c"
    }
};
```

In your rollbar-gem configuration:

```
Rollbar.configure do |config|
    # ... other configuration
    config.code_version = 'bdd2b9241f791fc9f134fb3244b40d452d2d7e35'
end
```

The other notifiers have very similar top-level code_version configuration settings. See the docs for your notifier for more info.

If you resolve an item within Rollbar in a certain version and also specify a code_version, we use both of these values to decide whether or not to reactivate the item.

For example: Let's say you have a bug in version 1.0 of your app. The bug is fixed and will be deployed to users in verision 1.1, but that won’t happen for a few days. You can just resolve the Rollbar item associated with this bug now, but also specify that the resolved version is 1.1. You will no longer get reactivation notifications for this item until occurrences of this item with a code_version >= 1.1 come in.


### Auto-resolving items in GitHub commits

If you connect Rollbar with GitHub, this process will also work with Git SHAs. We’ll query the GitHub API to determine whether one commit is a parent of the other.

You can now also include Rollbar item tags in your GitHub commit messages to automatically resolve them in the correct revision when deploying. Just include one of the following strings in your commits for each item you want to resolve:

```
fix $ref
fixed $ref
fixes $ref
resolve $ref
resolved $ref
resolves $ref
close $ref
closed $ref
closes $ref
```

Where `$ref` is one of the following item tags:

Full item URL, eg. `https://rollbar.com/item/123456789`
Item ID, eg. `rb#123456789`
Short item ID, eg. `rb#22` (This appears at the top left of an item page.)

Then execute a deploy by hitting the deploy API endpoint. The items referenced in any of the commit messages of the deploy will be resolved using the respective revision of that commit.