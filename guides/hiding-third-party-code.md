# Hiding Third-Party Code

When using libraries or frameworks you will often have large portions of well-tested third party
code that is unlikely to have caused an error for you. In order to keep the focus on your code
Rollbar will collapse stack frames from third party code.

![](https://d26gfdfi90p7cf.cloudfront.net/expand.152737.o.gif)

### Single Root

To set this up all you have to do is configure your notifier to send the `server.root`, or
the prefix URL for all in-house stack frame filenames. Any code from outside the `server.root`
directory will be collapsed by default when you load that item in the Rollbar UI.

For example, in a hypothetical stack trace with lines from the following files:

* `/home/deploy/www/app/model.py`
* `/home/deploy/www/app/controller.py`
* `/home/deploy/www/vendor/webfmwk/eventloop.py`
* `/home/deploy/www/vendor/webfmwk/startup.py`
* `/home/deploy/www/app/main.py`

and with `server.root` set to `/home/deploy/www/app`, the lines from the
`vendor` directory would be collapsed together, to allow you to focus on your code, and not the
unlikely possibility that `webfmk` has a bug.

### Extra Roots

Sometimes you'll have split your code into multiple sibling modules adjacent to folders
you do not want included as project code (vendor, models, controllers, for instance). In these cases
you can send additional application roots in the `project_package_paths` key. These paths should
look identical to the server root (the beginning of a URL), and the key should be in an array
containing any additional folders to be considered "in-project".
