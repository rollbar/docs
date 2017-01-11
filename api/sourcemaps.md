## Upload

	POST /api/1/sourcemap

### Form Data Parameters

Name | Type | Description
`access_token`|`string`|**Required** A `post_server_item`-scope project access token.
`version`|`string`|**Required** The current code version.
`minified_url`|`string`|**Required** The full URL of the minified file, as it appears in the stack trace. This should start with `http:` or `https:`.
`source_map`|`file upload`|**Required** Your source map file.
`source file paths`|`file upload`|The source files themselves.

### Example

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

## Trigger An Automatic Download

	POST /api/1/sourcemap/download

### Form Data Parameters

Name | Type | Description
`access_token`|`string`|**Required** A `post_server_item`-scope project access token.
`version`|`string`|**Required** The current code version.
`minified_url`|`string`|**Required** The full URL of the minified file, as it appears in the stack trace. This should start with `http:` or `https:`.


### Example

```
curl https://api.rollbar.com/api/1/sourcemap/download
	-F access_token=aaaabbbbccccddddeeeeffff00001111 \  
	-F version=92429d82a41e930486c6de5ebda9602d55c39986 \  
	-F minified_url=http://example.com/static/js/example.min.js
```