# Using Variables in Rollbar Notifications

Rollbar supports variables in notifications using a familiar `{{"{{VARIABLE_NAME"}}}}` syntax.  Different variable values are available depending on the type of event that triggers the notification.

## Usage Examples

_Default Deploy Message to Slack:_

`[{{"{{project_slug"}}}}] {{"{{username"}}}} deployed revision {{"{{revision"}}}} to {{"{{environment"}}}} {{"{{link"}}}}`

_Default Event title for Datadog:_

`[{{"{{project_slug"}}}}] {{"{{environment"}}}} - {{"{{trigger_description"}}}} {{"{{level"}}}}: {{"{{title"}}}}`

## Items
When an item has changed and triggered a notification, the following variables are available:

Variable | Description/Values
---------| ------------
`{{"{{link""}}}}` | Item URL
`{{"{{project_slug"}}}}` | Project name
`{{"{{title"}}}}` | Item title
`{{"{{summary"}}}}`| Item summary
`{{"{{markdown_summary"}}}}` | Items summary including markdown
`{{"{{environment"}}}}` | Environment reported in item (e.g. `production`, `staging`, etc.)
`{{"{{level"}}}}` | `Critical`, `Error`, `Warning`, `Info`, `Debug`
`{{"{{status"}}}}` | `Active`, `Resolved`, `Muted`
`{{"{{trigger_description"}}}}` | Description of event that triggered the notification
`{{"{{username"}}}}` | Rollbar user that triggered the notification (if any)
`{{"{{last_occurrence_time"}}}}` | Friendly-formatted timestamp of last occurrence (e.g. `1 minute ago`)
`{{"{{last_occurrence_link"}}}}` | Last occurrence URL

## Occurrences
When occurrences of an item trigger a notification, the following variables are available:

Variable | Description/Values
---------| ------------
`{{"{{project_slug"}}}}` | Project name
`{{"{{environment"}}}}` | Environment reported in item (e.g. `production`, `staging`, etc.)
`{{"{{title"}}}}`| Item title
`{{"{{level"}}}}` | `Critical`, `Error`, `Warning`, `Info`, `Debug`
`{{"{{status"}}}}` | `Active`, `Resolved`, `Muted`
`{{"{{occurrence_title"}}}}` | Same as item title
`{{"{{occurrence_link"}}}}` | Occurrence URL
`{{"{{PAYLOAD_DATA_FIELD"}}}}` | Any data value sent in the JSON payload may be used as a variable, including custom data.  For example, if your JSON payload includes {% comment %} {% highlight json %}{ "handler": { "key": "process-job", "id": 100}}{% endhighlight %}, then you can use the variables `{{"{{handler.key"}}}}` and `{{"{{handler.id"}}}}` in your notifications. {% endcomment %}


## Deploys
When a deploy triggers a notification, the following variables are available:

Variable | Description/Values
---------| ------------
`{{"{{project_slug"}}}}` | Project name
`{{"{{username"}}}}` | Rollbar user who triggered the deploy, or `unknown`
`{{"{{revision"}}}}` | Deployed revision
`{{"{{environment"}}}}` | Environment to which the deploy occurred (e.g. `production`, `staging`, etc.)
`{{"{{link"}}}}` | URL of deploy details in Rollbar
`{{"{{start_time"}}}}` | Deploy start time _(formatted based on project timezone setting)_
`{{"{{finish_time"}}}}`| Deploy finish time _(formatted based on project timezone setting)_
`{{"{{comment"}}}}` | Deploy comment
