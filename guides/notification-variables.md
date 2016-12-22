# Using Variables in Rollbar Notifications

Rollbar supports variables in notifications using a familiar ```{{VARIABLE_NAME}}``` syntax.  Different variable values are available depending on the type of event that triggers the notification.

## Items
When an item has changed and triggered a notification, the following variables are available:

Variable | Description/Values
---------| ------------
```{{link}}``` | Item URL
```{{project_slug}}``` | Project name
```{{title}}``` | Item title
```{{summary}}```| Item summary
```{{markdown_summary}}``` | ???
```{{environment}}``` | Environment reported in item (e.g. ```production```, ```staging```, etc.)
```{{level}}``` | ```Critical```, ```Error```, ```Warning```, ```Info```, ```Debug```
```{{status}}``` | ```Active```, ```Resolved```, ```Muted```
```{{trigger_description}}``` | Description of event that triggered the notification
```{{username}}``` | Rollbar user that triggered the notification (if any)
```{{last_occurrence_time}}``` | Friendly-formatted timestamp of last occurrence (e.g. ```1 minute ago```)
```{{last_occurrence_link}}``` | Last occurrence URL

## Occurrences
When occurrences of an item trigger a notification, the following variables are available:

Variable | Description/Values
---------| ------------
```{{project_slug}}``` | Project name
```{{environment}}``` | Environment reported in item (e.g. ```production```, ```staging```, etc.)
```{{title}}```| Item title
```{{level}}``` | ```Critical```, ```Error```, ```Warning```, ```Info```, ```Debug```
```{{status}}``` | ```Active```, ```Resolved```, ```Muted```
```{{occurrence_title}}``` | Same as item title
```{{occurrence_link}}``` | Occurrence URL
TODO | Explain what additional values are available on occurrences

## Deploys
When a deploy triggers a notification, the following variables are available:

Variable | Description/Values
---------| ------------
```{{project_slug}}``` | Project name
```{{username}}``` | Rollbar user who triggered the deploy, or ```unknown```
```{{revision}}``` | Deployed revision
```{{environment}}``` | Environment to which the deploy occurred (e.g. ```production```, ```staging```, etc.)
```{{link}}``` | URL of deploy details in Rollbar
```{{start_time}}``` | Deploy start time _(formatted based on project timezone setting)_
```{{finish_time}}```| Deploy finish time _(formatted based on project timezone setting)_
```{{comment}}``` | Deploy comment
