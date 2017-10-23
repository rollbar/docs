We recommend installing the Rollbar plugin through <a href="https://wpackagist.org/" target="_blank" rel="noopener">wpackagist</a> if you manage your project using Composer. This way ensures the plugin and all of its dependencies are managed by Composer.


1. If your WordPress project is not managed with Composer yet, we suggest looking into upgrading your WordPress: <a href="https://roots.io/using-composer-with-wordpress/" target="_blank" rel="noopener">Using Composer with WordPress</a>.

2. In your `composer.json` add `wpackagist-plugin/rollbar` to your `require` section, i.e.:
 
```
 "require": {
 "php": ">=5.5",
 ...,
 "wpackagist-plugin/rollbar": "*"
  }
```

3. Issue command `composer install` in the root directory of your WordPress project.

4. In `Plugins &rarr; Installed plugins` find `Rollbar` and click `Activate` underneath.

5. Copy the token value for your post_client_item and post_server_item. Your post_server_item access token is:

```
{{ server_access_token }}
```

Your post_client_item access token is:

```
{{ client_access_token }}
```

You can find these access tokens in the future by logging into your Rollbar account dashboard and going to `Settings → Project Access Tokens`.

6. Navigate to `Tools → Rollbar`.

7. Enable `PHP error logging` and/or `Javascript error logging` depending on your needs.

8. Paste the tokens you copied in step 5 in Access Token section.

9. Provide the name of your environment in `Environment`. By default, the environment will be taken from the `WP_ENV` environment variable if it's set, otherwise it's blank.

10. Pick a minimum logging level. Only errors at that or higher level will be reported. For reference: <a href="http://php.net/manual/en/errorfunc.constants.php" target="_blank" rel="noopener">PHP Manual: Predefined Error Constants</a>.

11. Click `Save Changes`.

For further information about the Wordpress plugin, see the docs <a href="https://rollbar.com/docs/notifier/rollbar-php-wordpress/" target="_blank" rel="noopener">here</a>. 
