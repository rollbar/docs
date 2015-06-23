<span class="date">03/02/15 at 11:13 AM</span>

How to Integrate Logstash with Rollbar
======================================

Logstash can send events collected from any log file to Rollbar.

Setup
-----

Setting up a complete Logstash system is beyond the scope of this
documentation. If you're new to Logstash, please see [Getting Started
with
Logstash](http://logstash.net/docs/1.4.2/tutorials/getting-started-with-logstash).

1.  Once you have Logstash working, install
    the [logstash-output-rollbar](https://github.com/rollbar/logstash-output-rollbar)
    plugin. As of March 1, 2015 the Logstash plugin system is [in
    transition](http://www.elasticsearch.org/blog/plugin-ecosystem-changes/).
    With the release of Logstash 1.5 installing plugins will be as
    simple as installing Ruby gems. In the meantime...

    If you're running Logstash **1.4.2**:
    :   Copy
        [rollbar.rb](https://github.com/rollbar/logstash-output-rollbar/blob/master/lib/logstash/outputs/rollbar.rb) to
        a directory in your
        [pluginpath](http://logstash.net/docs/1.4.2/flags). If you're
        simply experimenting, you can also drop rollbar.rb into your
        logstash installation's lib/logstash/outputs directory

    If you're running Logstash **1.5**:
    :   Install the Rollbar plugin with
         `$LS_HOME/bin/plugin install logstash-output-rollbar`

2.  Configure Logstash to send events to Rollbar (see Plugin
    Configuration below) 

Plugin Configuration 
---------------------

### Synopsis

This is what the Rollbar outconfiguration might look like in your
Logstash config file. Note that you can have multiple `rollbar` sections
within an `output` section to send different event types to different
projects, use different message formats, assign different Rollbar event
levels, ets.:

    output {
      rollbar {
        access_token => ... # password
        environment => ... # string (optional), default: "production"
        level => ... # string, one of ['debug', 'info', 'warning', 'error', 'critical'] (optional), default: "info"
        format => ... # string (optional), default: "%{message}"
        endpoint => ... # string (optional), default "https://api.rollbar.com/api/1/item"
      }
    }

### Details

**access\_token**
:   A Rollbar project access token. This can be the same
    `post_server_item` token you use elsewhere to configure other
    Rollbar plugins you may have installed, or you can create a new
    token. Note that you can have multiple rollbar output sections in
    your Logstash configuration file with different access token to
    route Logstash events to multiple Rollbar projects.

**environment**
:   The Rollbar project environment to use for events from this output

**level**
:   The event level to use for events from this output

**format**
:   The format string to use for generating the title of events in
    Rollbar. See "Using the Plugin" below.

**endpoint**
:   This is the URL for the Rollbar API endpoint. You shouldn't need to
    specify this value in your Logstash configuration.

Using the Plugin
----------------

Beyond configuring the plugin, you have a great deal of control over how
events will appear in Rollbar by adding fields to your Logstash event
using filters. Almost all the metadata for your Rollbar event can be
populated from Logstash event data.

For example, the **format** parameter above allows you to generate the
 Rollbar API data.body.message.body field from any fields in the
Logstash event (see examples below).

You can also add a `rollbar` field to your Logstash event to populate
other metadata fields in your Rollbar event.  The following Rollbar
events fields (described also [API Reference - Items
(POST)](https://rollbar.com/docs/api/items_post/) can be set based on
Logstash values.

-   platform
-   language
-   framework
-   context
-   request
-   person
-   server
-   client
-   fingerprint
-   title
-   uuid

Example Configuration
---------------------

The following example doesn't necessarily follow Logstash best practices
for filtering (the grok filters are rather cumbersome and should be
simplified using custom patterns), but it's a stand-alone example
demonstrating how you can collect multiple types of events from
Logstash, manipulate the fields of the Rollbar event, and pass events to
different Rollbar projects. 

You could generate events for the following logstash configuration using
the Python logstash shipper
[beaver](http://beaver.readthedocs.org) configured with:

    [beaver]
    logstash_version: 1
    tcp_host: logstashbox
    tcp_port: 9876
    format: json

    [/var/log/nginx/*.error.log]
    type: nginx_error
    add_field: project,RollbarAppProject

    [/var/log/mysql/mysql-slow.log]
    type: mysql_slow

 

Note that in the following Logstash configuration file, we're setting
`rollbar.request.user_ip`, `rollbar.platform`, and `rollbar.server.host`
to values extracted from the Logstash event.

    #
    # Collect JSON events sent via TCP to port 9876
    #
    input {
        tcp {
            host => '0.0.0.0'
            port => '9876'
            codec => json
        }
    }

    filter {

        # Nginx access logs assumed to be basic combined apache log format
        if [type] == "nginx_access" {
            grok {
                match => [ "message", "%{COMBINEDAPACHELOG}" ]
            }
        }

        # This nginx pattern matching should be broken out into customer patterns. As is,
        # it will match error lines with various combinations of fields and add
        # the client ip to the [rollbar][request][user_ip] field
        #
        if [type] == "nginx_error" {
            grok {
                match => [ "message", '^%{YEAR}/%{MONTHNUM}/%{MONTHDAY} %{HOUR}:%{MINUTE}:%{SECOND} \[%{LOGLEVEL:ngx_level}] %{NOTSPACE} %{NOTSPACE} %{DATA:ngx_msg}, client: %{IPORHOST:ngx_client}, server: %{IPORHOST:ngx_server}, request: "%{DATA:ngx_request}", upstream: "%{DATA:ngx_upstream}", host: %{DATA:ngx_host}, referrer: "%{DATA:ngx_referrer}"' ]
                match => [ "message", '^%{YEAR}/%{MONTHNUM}/%{MONTHDAY} %{HOUR}:%{MINUTE}:%{SECOND} \[%{LOGLEVEL:ngx_level}] %{NOTSPACE} %{NOTSPACE} %{DATA:ngx_msg}, client: %{IPORHOST:ngx_client}, server: %{IPORHOST:ngx_server}, request: "%{DATA:ngx_request}", upstream: "%{DATA:ngx_upstream}", host: %{DATA:ngx_host}' ]
                match => [ "message", '^%{YEAR}/%{MONTHNUM}/%{MONTHDAY} %{HOUR}:%{MINUTE}:%{SECOND} \[%{LOGLEVEL:ngx_level}] %{NOTSPACE} %{NOTSPACE} %{DATA:ngx_msg}, client: %{IPORHOST:ngx_client}, server: %{IPORHOST:ngx_server}, request: "%{DATA:ngx_request}", host: %{DATA:ngx_host}' ]
                match => [ "message", "^%{YEAR}/%{MONTHNUM}/%{MONTHDAY} %{HOUR}:%{MINUTE}:%{SECOND} \[%{LOGLEVEL:ngx_level}] %{NOTSPACE} %{NOTSPACE} %{DATA:ngx_msg}, client: %{IPORHOST:ngx_client}, server: %{HOSTPORT:ngx_server}" ]
                add_field => { "[rollbar][request][user_ip]" => "%{ngx_client}" }
            }
        }

        #
        # Adapted from http://www.phase2technology.com/blog/adding-mysql-slow-query-logs-to-logstash/
        #
        if [type] == "mysql_slow" {
            multiline {
                pattern => "^# User@Host:"
                negate => 'true'
                what => 'previous'
            }

            # Capture user, optional host and optional ip fields
            # sample log file lines:
            # User@Host: logstash[logstash] @ localhost [127.0.0.1]
            # User@Host: logstash[logstash] @  [127.0.0.1]
            grok {
                match => [ "message", "^# User@Host: %{USER:query_user}(?:\[[^\]]+\])?\s+@\s+%{HOST:query_host}?\s+\[%{IP:query_ip}?\]" ]
            }

            # Capture query time, lock time, rows returned and rows examined
            # sample log file lines:
            # Query_time: 102.413328  Lock_time: 0.000167 Rows_sent: 0  Rows_examined: 1970
            # Query_time: 1.113464  Lock_time: 0.000128 Rows_sent: 1  Rows_examined: 0
            grok {
                match => [ "message", "^# Query_time: %{NUMBER:query_time:float}\s+Lock_time: %{NUMBER:lock_wait:float} Rows_sent: %{NUMBER:rows_sent:int} \s*Rows_examined: %{NUMBER:rows_examined:int}"]
            }

            # Capture the time the query happened
            grok {
                match => [ "message", "^SET timestamp=%{NUMBER:timestamp};" ]
            }

            # Extract the time based on the time of the query and
            # not the time the item got logged
            date {
                match => [ "timestamp", "UNIX" ]
            }

            # Drop the captured timestamp field since it has been moved to the
            # time of the event
            mutate {
                remove_field => "timestamp"
            }
        }

        mutate {
            add_field => { "[rollbar][platform]" => "linux" }
            add_field => { "[rollbar][server][host]" => "%{host}" }
        }

    }

    output {

        # We use "in" instead of == to check the value of [project] because beaver
        # add_field actually adds an array, not a string

        if "RollbarAppProject" in [project] {

            # Access Token -> RollbarAppProject

            if [type] == "mysql_slow" {
                rollbar {
                    access_token => "ROLLBAR_APP_PROJECT_ACCESS_TOKEN"
                    format => "Slow MySQL Query"
                    level => 'warning'
                }
            }

            if [type] == "nginx_error" {
                rollbar {
                    access_token => "ROLLBAR_APP_PROJECT_ACCESS_TOKEN"
                    format => "Nginx Error: %{ngx_msg}"
                    level => 'error'
                }
            }

            if [type] == "nginx_access" {
                rollbar {
                    access_token => "ROLLBAR_APP_PROJECT_ACCESS_TOKEN"
                    format => "Nginx %{verb} %{request} from %{clientip}"
                    level => 'info'
                }
            }

        } else {

            # Access Token -> Default Rollbar project

            if [type] == "mysql_slow" {
                rollbar {
                    access_token => "DEFAULT_ACCESS_TOKEN"
                    format => "Slow MySQL Query"
                    level => 'warning'
                }
            }

            if [type] == "nginx_error" {
                rollbar {
                    access_token => "DEFAULT_ACCESS_TOKEN"
                    format => "Nginx Error: %{ngx_msg}"
                    level => 'error'
                }
            }

            if [type] == "nginx_access" {
                rollbar {
                    access_token => "DEFAULT_ACCESS_TOKEN"
                    format => "Nginx %{verb} %{request} from %{clientip}"
                    level => 'info'
                }
            }

        }
    }
