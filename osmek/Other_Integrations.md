<span class="date">05/21/14 at 08:27 PM</span>

Clojure
-------

For Clojure, try [rollcage](https://github.com/circleci/rollcage) by
[Marc O'Morian](https://github.com/marcomorain) from
[CircleCI](https://circleci.com) or [crowboar](https://github.com/mcohen01/crowbar) by [Michael
Cohen](https://github.com/mcohen01).

Dart
----

For Dart, use [rollbar.dart](https://github.com/Mixbook/rollbar.dart) by
Anton Astashov
from [Mixbook](http://www.mixbook.com/?utm_source=rollbar&utm_medium=docs&utm_campaign=friends).

Erlang
------

For Erlang, use [erollbar](https://github.com/omarkj/erollbar) by Omar
Yasin
from [Heroku](https://www.heroku.com/?utm_source=rollbar&utm_medium=docs&utm_campaign=friends).

Go
--

For Go, check out [go-rollbar](https://github.com/stvp/rollbar) by Tyson
from [Stovepipe
Studios](http://www.stovepipestudios.com/?utm_source=rollbar&utm_medium=docs&utm_campaign=friends).

Haskell
-------

For Haskell,
use [rollbar-haskell](https://github.com/docmunch/rollbar-haskell) by
Greg Weber
from [Docmunch](https://www.docmunch.com/?utm_source=rollbar&utm_medium=docs&utm_campaign=friends).
Also available
on [Hackage](http://hackage.haskell.org/package/rollbar-0.3).

Java
----

For Java, try
[rollbar-logback](https://github.com/tapstream/rollbar-logback) by
Tapstream
or [rollbar-java](https://github.com/rafael-munoz/rollbar-java) by
Rafael Munoz. If you use Maven, try
[rollbar-maven](https://github.com/borjafpa/rollbar-maven) by Borja
Pernia.

For Google App Engine,
try [rollbar-appengine](https://github.com/stickfigure/rollbar-appengine) by
Jeff Schnitzer.

.NET
----

For .NET, check
out [RollbarSharp](https://github.com/mroach/RollbarSharp) on GitHub.
It's maintained by the community and currently in a "preview release"
state, but is being actively developed.

Perl
----

For Perl,
find [WebService::Rollbar::Notifier](https://metacpan.org/pod/WebService::Rollbar::Notifier) on
CPAN.

ColdFusion
----------

For ColdFusion, check
out [rollbarcfc](https://github.com/jboursiquot/rollbarcfc) by [@jboursiquot](https://twitter.com/jboursiquot).
It's well-documented and being used in production.

Server-side log files
---------------------

**rollbar-agent** is a process that runs server-side, monitors log
files, and sends events of interest to Rollbar. It runs as a standalone
process and no application-specific integration is required.

Installation and configuration instructions are on the [GitHub project
page](http://github.com/rollbar/rollbar-agent).

Airbrake-compatible
-------------------

We have an API endpoint that is wire-compatible with the Airbrake
Notices API v2.2. If you are currently an Airbrake user, this may be
your easiest way to get started.

To use, configure your library to use the host api.rollbar.com (if it is
configured with a host) or the
URLhttps://api.rollbar.com/notifier\_api/v2/notices (if it is configured
with a URL).

For example, if using the Airbrake Rails gem, put the following
in config/initializers/airbrake.rb:

``` {data-language="ruby"}
Airbrake.configure do |config|
  config.api_key = 'YOUR_PROJECT_ACCESS_TOKEN'
  config.host = 'api.rollbar.com'
  config.secure = true
end
```

Not all Rollbar features are available through this endpoint, so when
possible we recommend using a Rollbar-specific library instead.

Other Platforms
---------------

If we don't have a notifier for your language or platform, please email
us
at [team@rollbar.com](mailto:team@rollbar.com?subject=Please+make+a+notifier+for+my+platform).

You can also integrate directly with our API. [View the
documentation](https://rollbar.com/docs/api_items/).
