# Custom Log Messages

You can send any log message to Rollbar, not just exceptions. Log messages can have the same
attached metadata as exceptions (request, server, person, etc.) and go through a similar
de-duplication process as exceptions.

Log messages have a level (`critical`, `error`, `warning`,
`info`, or `debug`), a body (just a string), and any arbitrary optional
parameters you want to include.

* {: .active} [Ruby](#ruby)
* [Python](#python)
* [PHP](#php)
* [Node.js](#nodejs)
* [Javascript](#javascript)
{: .nav .nav-tabs}

<div class="tab-content">

```ruby
# log methods exist for each level, or pass as a param
Rollbar.critical("Crash while processing payment")
Rollbar.log("error", "Crash while checking order status")
Rollbar.warning("Facebook API unavailable")
Rollbar.info("User logged in")
Rollbar.debug("Cron job starting")

# can pass arbitrary params
Rollbar.info("User logged in", :login_type => "email+password")

# rich metadata will be included automatically, but if you want to override:
Rollbar.scope(person => {:id => "123"}).info("User logged in")
```
{: .tab-pane .active #ruby}

```python
# default level is 'error'
rollbar.report_message('Got an IOError in the main loop')

# logs at the 'warning' level
rollbar.report_message('Got an IOError in the main loop', 'warning')

# can also include the request object
rollbar.report_message('Got an IOError in the main loop', 'warning', request)

# or extra context
rollbar.report_message('Got an IOError in the main loop', 'warning', extra_data={'job_id': job_id})
```
{: .tab-pane #python}

```php
<?php
// default level is 'error'
Rollbar::report_message('Could not connect to database');

// logs as the 'warning' level
Rollbar::report_message('Could not connect to Facebook API', 'warning');
```
{: .tab-pane #php}

```js
// default level is 'error'
rollbar.reportMessage("Could not connect to database");

// logs at the 'warning' level
rollbar.reportMessage("Could not connect to memcache", "warning");
```
{: .tab-pane #nodejs}

```js
// log methods exist for each level, or pass as a param
Rollbar.critical("Crash while processing payment");
Rollbar.log("error", "Crash while checking order status");
Rollbar.warning("Facebook API unavailable");
Rollbar.info("User logged in");
Rollbar.debug("Cron job starting");

// can pass arbitrary params
Rollbar.info("User logged in", {loginType: "email+password"});

// rich metadata will be included automatically, but if you want to override:
Rollbar.scope({person: {id: "123"}}).info("User logged in");
```
{: .tab-pane #javascript}

</div>

For more details, please see our [documentation](https://rollbar.com/docs/).
