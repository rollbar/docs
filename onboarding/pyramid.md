1. Install [pyrollbar](https://github.com/rollbar/pyrollbar) with [pip](http://pip.readthedocs.org/en/stable/quickstart/):

    ```python
    pip install rollbar
    ```

2. In your ``ini`` file (e.g. ``production.ini``), add ``rollbar.contrib.pyramid`` to the end of your ``pyramid.includes``:

    ```ini
    [app:main]
    pyramid.includes =
        pyramid_debugtoolbar
        rollbar.contrib.pyramid
    ```
      
3. Add these rollbar configuration variables:

    ```ini
    [app:main]
    rollbar.access_token = {{ server_access_token }}
    rollbar.environment = production
    rollbar.branch = master
    rollbar.root = %(here)s
    ```

4. Send a test message using pshell.

    ```shell
    $ pshell development.ini
    > import rollbar
    > rollbar.report_message("hello world")
    ```
