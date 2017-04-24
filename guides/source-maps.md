# Source Maps

If you minify your JavaScript code for use in production, you may be seeing Rollbar errors that reference the
minified code, not the original source code.  In order to display stack traces with your original code, Rollbar needs access to the source maps for your minified Javascript.

Benefits of providing your source maps to Rollbar include:

-   in stack traces, you'll see the original source filename, line
    number, method name, and code snippet so you can debug more easily
-   error grouping should be more resilient to code changes

## Source Map Requirements

For the minified-to-source translation to work, we need:

-   **A stack trace with column numbers**

    You'll get one of these if you give Rollbar an Error object, in a
    browser that provides column numbers. Like this:

    ```js
    try {
      throw new Error("Something went wrong");
    } catch (e) {
      Rollbar.error(e);
    }
    ```

    As far as we can tell, this currently works for caught errors in
    Chrome, IE10, and Firefox.

    Uncaught errors (reported by the browser's top-level error handler,
    window.onerror) will have column numbers in the newest versions of
    Chrome and Firefox. The HTML5 Spec has been updated to require this,
    so other browsers may add this support in the future.

-   **A source map file, along with (optionally) any or all of the
    original source files referenced by the source map**

    We'll call this all together a "source map package". It can either
    be uploaded directly to us via an API call, or downloaded by us when
    we encounter errors in minified files that source map url comment
    directives.

    You'll need to generate source maps, if you aren't already. This can
    be done using tools like the [Closure
    Compiler](https://developers.google.com/closure/compiler/) or [UglifyJS
    2](https://github.com/mishoo/UglifyJS2).

    You can include the source inside the source map. We'll look for it in `sourcesContent` as per the source map standard.

## Enabling Source Map Translation in Rollbar

Add these two parameters to the `_rollbarConfig` object that you have
included in the on-page Javascript snippet:

```js
var _rollbarConfig = {
  // add these new params:
  payload: {
    client: {
      javascript: {
        source_map_enabled: true,
        code_version: "some version string, such as a version number or git sha",
        // Optionally have Rollbar guess which frames the error was thrown from
        // when the browser does not provide line and column numbers.
        guess_uncaught_frames: true
      }
    }
  }
};
```

If you need to set this configuration after the Rollbar library has been
initialized, use `Rollbar.configure()`:

```js
Rollbar.configure({
  payload: {
    client: {
      javascript: {
        source_map_enabled: true,
        code_version: "some version string, such as a version number or git sha",
        guess_uncaught_frames: true
      }
    }
  }
});
```

## Providing Source Maps to Rollbar

We recommend that you upload source maps to Rollbar prior to each production deployment, however we can also attempt to download them automatically based on configuration data in your minifed Javascript files. 

### Recommended Method: Upload pre-deploy

At the beginning of your deploy script (before the new code is in
production), upload a source map package via our API.

Here's an example cURL command:

```bash
curl https://api.rollbar.com/api/1/sourcemap \
  -F access_token=aaaabbbbccccddddeeeeffff00001111 \
  -F version=version_string_here \
  -F minified_url=http://example.com/static/js/example.min.js \
  -F source_map=@static/js/example.min.map \
  -F static/js/site.js=@static/js/site.js \
  -F static/js/util.js=@static/js/util.js
```

#### Params

access\_token
:   Your rollbar access token. Should be a post\_server\_item token (the
    same one that you use for sending deploy notifications).

version
:   A string identifying what version of your code this source map
    package is for. We recommend using the version number/string from
    your version control system, e.g. a full Git SHA.\
     Note that you will need to pass this same string in the on-page JS
    snippet, as documented above.

minified\_url
:   The full URL of the minified file. Should start with http: or
    https:, which we'll strip off.

source\_map
:   The contents of the source map, as a multipart file upload.

(each source file)
:   (Optional) Param name should be the path to the unminified JS file,
    as defined in the source map.\
     Value should be the contents of the source file, as a multipart
    file upload.

#### Response Codes

200 OK
:   Upload received successfully.

422 Unprocessable Entity
:   There was an error validating the upload. The error message should
    contain details of what went wrong.

We store the source map package by project+version+minified URL. If you
upload it more than once, each subsequent upload will overwrite the
previous data.

**Explanation of the example**

In the above example:

-   Our website is `http://example.com`
-   We have a minified javascript file at
    `http://example.com/js/example.min.js`
-   We have a source tree like this:\

        example/
        example/static/js/example.min.js
        example/static/js/example.min.map
        example/static/js/site.js
        example/static/js/util.js

-   We built our minified file (`static/js/example.min.js`) and source
    map (`static/js/example.min.map`) by running the Closure Compiler
    from `example/`. It contains code from `static/js/site.js` and
    `static/js/util.js`.

Here's an example Closure Compiler command run from `example/` to
generate the above files:

```bash
java -jar compiler.jar --js static/js/site.js --js static/js/util.js --js_output_file static/js/example.min.js --create_source_map static/js/example.min.map
```

NOTE: if using the `sourceMappingURL` method, you will need to add this
comment manually to the bottom of the generated minified file, as
Closure Compiler doesn't provide a way to do this automatically.

Here is the same command for UglifyJS2:

```bash
uglifyjs static/js/site.js static/js/util.js --output static/js/example.min.js --source-map static/js/example.min.map
```


### Alternative Method: Automatic download

As specified in the [Source Map
Specification](https://docs.google.com/document/d/1U1RGAehQwRypUTovF1KRlpiOFze0b-_2gc6fAH0KY0k/edit),
you should place a comment like the following at the bottom of your
minified JavaScript files:

```js
//# sourceMappingURL=URL_TO_SOURCE_MAP
```
**How it works:** If we receive a JavaScript error, source maps are
enabled, and we don't already have the source map for the current code
version, we will schedule an attempt to download it. For each stack
frame, we'll first download the minified source file and look for a
`sourceMappingUrl` comment. If it has one, we'll try to download that
file and save it as the source map. Then for future errors, we'll use
the source map to translate the minified frames back to original frames.

This is the easiest method, but not suitable for all cases (i.e. if you
don't want to expose your source map or code to the public web). It is
also less reliable than the upload method, since the source map won't be
downloaded yet when the first few errors come in. We recommend the
upload method for production use.

#### Triggering an automatic download

If you're using the Automatic Download method, you can notify our API to
trigger a download for each of your minified files. Doing this will
reduce the number of errors that the source map isn't applied to (since
we'll have a greater chance of downloading the source map before the
first error after a deploy occurs).

Here is a sample command:

```bash
curl https://api.rollbar.com/api/1/sourcemap/download
  -F access_token=aaaabbbbccccddddeeeeffff00001111 \  
  -F version=92429d82a41e930486c6de5ebda9602d55c39986 \  
  -F minified_url=http://example.com/static/js/example.min.js
```

##### Params

access\_token
:   Your rollbar access token. Should be a post\_server\_item token (the
    same one that you use for sending deploy notifications).

version
:   A string identifying what version of your code this source map
    package is for. We recommend using the version number/string from
    your version control system, e.g. a full Git SHA. Must be the same
    string as in the on-page JS snippet, as documented above.

minified\_url
:   The full URL of the minified file. Should start with `http:` or
    `https:`

## Using Source Maps On Many Domains

If you'd like to use source maps with the same code that is deployed on many domains, use the following code:

```javascript
var _rollbarConfig = {
  // ...
  transform: function(payload) {
    var trace = payload.data.body.trace;
    // Change 'yourdomainhere' to your domain.
    var locRegex = /^(https?):\/\/[a-zA-Z0-9._-]+\.yourdomainhere\.com(.*)/;
    if (trace && trace.frames) {
      for (var i = 0; i < trace.frames.length; i++) {
        var filename = trace.frames[i].filename;
        if (filename) {
          var m = filename.match(locRegex);
          // Be sure that the minified_url when uploading includes 'dynamichost'
          trace.frames[i].filename = m[1] + '://dynamichost' + m[2];          
        }
      }
    }
  }
}

```

Be sure to change your hostname in the `minified_url` parameter to `dynamichost` when uploading your source map files:

```bash
curl https://api.rollbar.com/api/1/sourcemap \
  -F access_token=aaaabbbbccccddddeeeeffff00001111 \
  -F version=version_string_here \
  -F minified_url=http://dynamichost/static/js/example.min.js \
  -F source_map=@static/js/example.min.map \
  -F static/js/site.js=@static/js/site.js \
  -F static/js/util.js=@static/js/util.js
```

## Managing Source Maps

Source maps are stored per project, and are accessible by going to **Project Settings --> Source Maps**

Within the source maps screen for a project, you can:
* View all source map access attempts, including failed attempts to upload/download.
* Download source maps.
* Delete source maps.
* Search for source maps based on `code_version` or the name of the associated Javascript file.

## Source Map Resources

Members of the Rollbar community have created some plugins to integrate
the source map upload step into their build process. The Rollbar team
does not maintain them, but we are happy to provide support to maintainers.

Build System | Link
-------------|-----
Gulp|[gulp-rollbar](https://github.com/ismriv/gulp-rollbar)
Webpack|[rollbar-sourcemap-webpack-plugin](https://github.com/thredup/rollbar-sourcemap-webpack-plugin)

If you've written a plugin or other resource that you'd like us to link here,
please let us know! Send us an email at <support@rollbar.com>

## Source Map FAQ

### What if I have more than one minified file?
{: .no_toc}

That's fine -- just upload a source map package for each minified file,
each time your code version changes. Note that the code version is
global to your project, so you will have to upload the package for each
one every time you deploy, even if only one of them changed.

### Does it matter what tool I used to build the source map?
{: .no_toc}

It shouldn't, as long as the tool builds source maps adhering the V3 of the source map spec.

We've tested with [Closure
Compiler](https://developers.google.com/closure/compiler/) and [UglifyJS
2](https://github.com/mishoo/UglifyJS2). If you're using something else
and having problems, please let us know.

### What happens if I don't upload the source map package?
{: .no_toc}

We'll still process incoming errors immediately, but skip the
minified-to-source translation.

### Where is my data stored?
{: .no_toc}

The source map package (including the source map itself and any source
files you upload) is stored in our MySQL cluster. We encrypt the
contents with AES-256-CBC.

Derived data is stored on our dedicated hardware in the clear. This
includes:

-   file-line-column mappings, stored in Memcache
-   un-minified file, line, column, and code snippet, stored in our
    MySQL cluster

### It's not working. How can I debug this?
{: .no_toc}

Here are a few common problems:

-   Missing one or both of the config params in the on-page JS snippet.
    See Step 1 and make sure you're setting both
    `payload.client.javascript.source_map_enabled` and
    `payload.client.javascript.code_version`
-   If using the Upload method: code\_version used in the one-page
    snippet does not match the version provided in the upload call
-   If using the Download method: source map file or minified javascript
    source files are on a host that's not reachable from the public
    internet, or are gated behind an authorization wall. Fix: use the
    Upload method instead.
-   The Javascript error that you are expecting to be un-minified does
    not have column numbers, and you haven't enabled
    `guess_uncaught_frames`. We need column numbers to be able to apply
    the source map without guessing--see the first section of "Basic
    Setup" above for more details.
-   Some source map generation tools support an alternate representation
    of the map that combines multiple sub-maps into "sections" within
    the top level map. Each section can either be embedded source map or
    a reference to an external source map. Unfortunately, we don't yet
    support this source map format.
-   Don't forget to update the version number when you update your JavaScript.
    If you don't, the filename, line and column numbers will be incorrect.
-   The value of `minified_url` must be the full URL of the minified file.
    This should start with `http:` or `https:`, which we'll strip off.
-   If you're a Rails asset pipeline user, be sure you aren't generating source
    maps off an already minified file.  
    
 If your still not able to get source maps working, we're here to help!  Simply message us via the in-app chat or email <support@rollbar.com>
