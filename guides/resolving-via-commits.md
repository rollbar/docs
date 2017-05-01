# Resolving via Commit Messages

If your project is integrated with [GitHub](/docs/github/), [Bitbucket](/docs/bitbucket), or [GitLab](/docs/gitlab/) then you can include Rollbar item
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

-   Full item URL, eg. `https://rollbar.com/rivkah/Test-PHP/items/2/`
-   Item ID, eg. `rb#123456789`

Then execute a deploy by hitting the [deploy API endpoint](https://rollbar.com/docs/deploys/bash/).
The items referenced in any of the commit messages of the deploy will be resolved using the
revision specified in the deploy params.
