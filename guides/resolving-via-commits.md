If your project is integrated with GitHub, you can include Rollbar item
identifiers in your commit messages to auto-resolve the associated items
when deploying.

Just include one of the following strings for each item you want to
resolve in a commit message:

-   fix \$ref
-   fixed \$ref
-   fixes \$ref
-   resolve \$ref
-   resolved \$ref
-   resolves \$ref
-   close \$ref
-   closed \$ref
-   closes \$ref

 Where `$ref` is one of the following:

-   Full item URL, eg. `https://rollbar.com/item/123456789`
-   Item ID, eg. `rb#123456789`
-   Short item ID, eg. `rb#22` This appears at the top left of an item
    page.

Then execute a deploy by hitting the [deploy API endpoint](https://rollbar.com/docs/deploys/bash/).
The items referenced in any of the commit messages of the deploy will be resolved using the
revision specified in the deploy params.
