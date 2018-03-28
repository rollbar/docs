---
title: Person Tracking
---

# People Tracking

Rollbar can track which of your People (users) are affected by each error. This works automatically
in our Rails and Django libraries, and is easy to set up for the rest.

You can see which people were affected by any one error:

![](../images/guides/person-tracking/people_item.png)

Or the history of errors experienced by a particular person:

![](../images/guides/person-tracking/person_detail.png)

As well as the list of all people who have ever experienced an error, sorted by most recent error:

![](../images/guides/person-tracking/people_project.png)


<ul class="blog nav nav-tabs">
  <li role="presentation">
    <a href="#python" aria-controls="panel-1-1" role="tab" data-toggle="tab">Python</a>
  </li>
  <li role="presentation">
    <a href="#ruby" aria-controls="panel-1-2" role="tab" data-toggle="tab">Ruby</a>
  </li>
  <li role="presentation">
    <a href="#php" aria-controls="panel-1-3" role="tab" data-toggle="tab">PHP</a>
  </li>
  <li role="presentation">
    <a href="#node" aria-controls="panel-1-4" role="tab" data-toggle="tab">Node</a>
  </li>
  <li role="presentation">
    <a href="#dotnet" aria-controls="panel-1-5" role="tab" data-toggle="tab">.NET</a>
  </li>
  <li role="presentation">
    <a href="#java" aria-controls="panel-1-6" role="tab" data-toggle="tab">Java</a>
  </li>
  <li role="presentation">
    <a href="#js" aria-controls="panel-1-7" role="tab" data-toggle="tab">Browser JS</a>
  </li>
  <li role="presentation">
    <a href="#ios" aria-controls="panel-1-8" role="tab" data-toggle="tab">iOS</a>
  </li>
  <li role="presentation">
    <a href="#android" aria-controls="panel-1-9" role="tab" data-toggle="tab">Android</a>
  </li>
  <li role="presentation">
    <a href="#flash" aria-controls="panel-1-10" role="tab" data-toggle="tab">Flash</a>
  </li>
</ul>

<div class="tab-panel" id="panel-1-1"></div>

```python

# Pyrollbar works by inspecting the `request` for a `rollbar_person`,
# `user` or `user_id` field (in that order). The first one it finds
# it uses as the person data assuming the object contains at least
# the `id` field.

# For a request with only a `user_id` field, the person is sent as
# follows: `{ id: request.user_id }`.

# Many/Most frameworks handle this all automatically.

```

<div class="tab-panel" id="panel-1-2"></div>

```ruby
# For more documentation see:
# https://rollbar.com/docs/notifier/rollbar-gem/#person-tracking

# In Rails, Rollbar will automatically call the `current_user` method
# on the controller. The method name can be overridden in the Rollbar
# configuration:

Rollbar.configure do |config|
 config.person_method = 'current_user_override'
end

# The returned object should have `id`, `email`, and `username`
# methods. These method names can be overridden in the Rollbar
# configuration:

Rollbar.configure do |config|
  config.person_id_method = 'get_id'
  config.person_username_method = 'get_username'
  config.person_email_method = 'primary_email'
end

# If you are *not* using Rails, Rollbar will automatically pick up
# the `rollbar.person_data` key in the Rack environment and pass it
# on to the Rollbar website. It *must* have at least an `id` field.
# `username` and `email` will also be treated specially.
```


<div class="tab-panel" id="panel-1-3"></div>

```php
<?php
function get_current_user() {
    if ($_SESSION['user_id']) {
        return array(
            'id' => $_SESSION['user_id'], // required - value is a string
            'username' => $_SESSION['username'], // optional - value is a string
            'email' => $_SESSION['user_email'] // optional - value is a string
        );
    }
    return null;
}
$config['person_fn'] = 'get_current_user';
?>
```


<div class="tab-panel" id="panel-1-4"></div>

```js
// rollbar.js works by inspecting the `request` for a `rollbar_person`,
// `user` or `user_id` field (in that order). The first one it finds
// it uses as the person data assuming the object contains at least
// the `id` field. Both `email` and `username` are also specially treated.

/**
* This is a pretend function that gets called before the handler for the
* request itself. It adds the appropriate object to the request so Rollbar
* can send the person data
*/
function beforeRequestHandler(request) {
  request.rollbar_person = {
    id: 42,
    email: 'dadams@example.com',
    username: 'dadams'
  }
}

// For a request with only a `user_id` field, the person is sent as
// follows: `{ id: request.user_id }`. If `user_id` is a function it will
// be evaluated before sending.

// If you are using the Passport authentication library no additional
// configuration is needed to make this work as expected.
```

<div class="tab-panel" id="panel-1-5"></div>

```
Rollbar.PersonData(() => new Person
{
    Id = 123, // required
    Username = "rollbar",
    Email = "user@rollbar.com"
});
```


<div class="tab-panel" id="panel-1-6"></div>

```java
import com.rollbar.Rollbar;
import com.rollbar.payload.data.Person;

public class HelloWorld {
    public static final Rollbar rollbar = new Rollbar(<token>, <env>);
    public static void main(String[] args) {
        Person person = new Person();
        Rollbar personRollbar = rollbar.person(person);
    }
}
```

<div class="tab-panel" id="panel-1-7"></div>

```js

// To track the current user in Javascript you can alter your `_rollbarConfig`
// like so:

var _rollbarConfig = {
  // The usual
  payload: {
    // The usual
    person: {
      id: 42, // required 
      username: 'dadams',
      email: 'dadams@example.com'
    }
  }
}

// If you've already initialized Rollbar and need to set the user *after*
// initialization has already occurred you can use the `configure` method:

Rollbar.configure({
  payload: {
    person: {
      id: 456, // required
      username: "foo",
      email: "foo@example.com"
    }
  }
});
```

<div class="tab-panel" id="panel-1-8"></div>

```objective_c
// In order to record the current user in an iOS application you must call
// `initWithAccessToken` with the optional `RollbarConfiguration` object.

// Something like this will work:

RollbarConfiguration *config = [RollbarConfiguration configuration];
[config setPersonId:@"42", username:"dadams", email:"dadams@example.com"];

[Rollbar initWithAccessToken:@"POST_CLIENT_ITEM_ACCESS_TOKEN" configuration:config];

// If you've already initialized the gem, you can update the person later by
// getting the `config` object and calling `setPersonId` on it:

[config setPersonId:@"42", username:"dadams", email:"dadams@example.com"];

The person ID is required.
```


<div class="tab-panel" id="panel-1-9"></div>

```java
// After initializing Rollbar you can configure the person with the `setPersonData` method:

@Override
public void onCreate(Bundle savedInstanceState) {
    /** The Usual **/
    Rollbar.init(this, POST_CLIENT_ITEM_ACCESS_TOKEN, ENVIRONMENT);
    Rollbar.setPersonData(CurrentUser.id, CurrentUser.username, CurrentUser.email);
}

// The methods `getUserId()`, `getUsername()` and `getEmail()` should return strings. If the
// `id` method returns null then no person will be recorded. Username and email are optional.
```


<div class="tab-panel" id="panel-1-10"></div>

```actionscript
// In flash you must configure the Rollbar person when first initializing the
// SDK. The fourth argument to `Rollbar.init` is `person`. This argument
// can be passed an id string, an object, or a function (which returns an
// appropriate object). The id is required.

Rollbar.init(this, accessToken, environment, "42"); //For user, id 42

// or
var person:Object = {
  id: 42,
  email: 'dadams@example.com',
  username: 'dadams'
};
Rollbar.init(this, accessToken, environment, person);

// or
function getCurrentUser() {
  return {
    id: 42,
    email: 'dadams@example.com',
    username: 'dadams'
  };
}
Rollbar.init(this, accessToken, environment, getCurrentUser); //For user, id 42
```

