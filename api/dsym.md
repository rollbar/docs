## Upload your .dSYM files

	POST /api/1/dsym

Requires `post_server_item` scope.

### Form Data Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required** A `post_server_item`-scope project access token.
`bundle_identifier`|`string`|**Required** The current code version.
`dsym`|`file name`|**Required** Your zipped dSYM file. See [here](https://raw.githubusercontent.com/rollbar/rollbar-ios/master/upload_dsym.py) for more info.

### Example

```bash
curl -X POST "https://api.rollbar.com/api/1/dsym"
	-F access_token=POST_SERVER_ITEM_ACCESS_TOKEN \
	-F version=0.1.2 \
	-F bundle_identifier="com.apple.xcode.dsym.org.rollbar.DelightfulApp" \
	-F dsym=dsym.zip \
```