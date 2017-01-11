## Upload a ProGuard Mapping file

	POST /api/1/proguard

### Form Data Parameters

Name | Type | Description
-----|------|-------------
`access_token`|`string`|**Required** A `post_server_item`-scope project access token.
`version`|`string`|**Required** The current code version. This must match the `android:versionName` in your app's `AndroidManifest.xml`, corresponding to the version the `mapping.txt` was generated for.
`mapping`|`file upload`|**Required** Your `mapping.txt` file.

### Example

```bash
curl 'https://api.rollbar.com/api/1/proguard' \
	-F access_token=POST_SERVER_ITEM_ACCESS_TOKEN \
	-F version=0.0.10 \
	-F mapping=mapping.txt
```