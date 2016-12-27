To upload your .dSYM files, POST to the the `api/1/dsym` endpoint with the following params:

access_token
:	your `post_server_item` access token

version
:	a string indicating the current code version.

bundle_identifier
:	your bundle identifier

dsym
:	path to your zipped dSYM file. See [here](https://raw.githubusercontent.com/rollbar/rollbar-ios/master/upload_dsym.py) for more info on this.


Here is an example cURL command to upload your .dSYM files:

```bash
curl -X POST "https://api.rollbar.com/api/1/dsym"
	-F access_token=POST_SERVER_ITEM_ACCESS_TOKEN \
	-F version=0.1.2 \
	-F bundle_identifier="com.apple.xcode.dsym.org.rollbar.DelightfulApp" \
	-F dsym=@path/to/dsym.zip" \
```