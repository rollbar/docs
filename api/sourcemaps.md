These calls require a project-level access token, which should be provided in the query string. The prefix for all URLs is `https://api.rollbar.com`.

# Upload

To upload your source maps at the beginning of your deploy script (before the new code is in production), call the `api/1/sourcemap` endpoint with the following params:

access_token
:	a project-level access token

version
:	a string indicating the current code version

minified_url
:	the full URL of the minified file. This should start with `http:` or `https:`, which we'll strip off.

source_map
:	the URL for the source map file

other params 
:	as needed for your source tree.

Example:

```bash
curl https://api.rollbar.com/api/1/sourcemap \
    -F access_token=aaaabbbbccccddddeeeeffff00001111 \
    -F version=version_string_here \
    -F minified_url=http://example.com/static/js/example.min.js \
    -F source_map=@static/js/example.min.map \
    -F static/js/site.js=@static/js/site.js \
    -F static/js/util.js=@static/js/util.js
```

In the above example, our website is `http://example.com`, we have a minified JavaScript file at `http://example.com/js/example.min.js`, and we have a source tree like this:

```
example/
example/static/js/example.min.js
example/static/js/example.min.map
example/static/js/site.js
example/static/js/util.js
```

# Download

You can notify our API to trigger a download for each of your minified files. 

Call the `api/1/sourcemap` endpoint with the following params:

access_token

version
:	a string indicating the current code version

minified_url
:	the full URL of the minified file. This should start with `http:` or `https:`, which we'll strip off.


Example:

```
curl https://api.rollbar.com/api/1/sourcemap/download
	-F access_token=aaaabbbbccccddddeeeeffff00001111 \  
    -F version=92429d82a41e930486c6de5ebda9602d55c39986 \  
    -F minified_url=http://example.com/static/js/example.min.js
```