## Upload an iOS .dSYM file

	POST /api/1/dsym

This is usually done via the [upload_dsym.py](https://raw.githubusercontent.com/rollbar/rollbar-ios/master/upload_dsym.py) script. For more information on this, see the "Symbolication using .dSYM files" section of our [iOS notifier docs](https://rollbar.com/docs/notifier/rollbar-ios/).

### Form Data Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required** A `post_server_item`-scope project access token.
`bundle_identifier`|`string`|**Required** The current code version.
`dsym`|`file upload`|**Required** Your zipped dSYM file. See [here](https://raw.githubusercontent.com/rollbar/rollbar-ios/master/upload_dsym.py) for more info.

### Example

```bash
curl -X POST "https://api.rollbar.com/api/1/dsym"
	-F access_token=POST_SERVER_ITEM_ACCESS_TOKEN \
	-F version=0.1.2 \
	-F bundle_identifier="com.apple.xcode.dsym.org.rollbar.DelightfulApp" \
	-F dsym=dsym.zip
```