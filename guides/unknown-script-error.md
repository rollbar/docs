# Summary
This happens when your JS code is hosted on a different domain (i.e. a CDN). To fix, set `Access-Control-Allow-Origin: *` on the JS file, and `crossorigin="anonymous"` on the `<script>` tag.  

If the script errors are coming from Javascript that you don't maintain, you can suppress them using the [ignoreMessages option in Rollbar.js](/docs/notifier/rollbar.js/#ignoring-specific-exception-messages)

# Full explanation
`"Script Error"` happens when an uncaught JavaScript error crosses domain boundaries in violation of the cross-origin policy. For example, if you host your JavaScript code on a CDN, any uncaught errors (errors that bubble up to the `window.onerror` handler, instead of being caught in `try-catch`) will get reported as simply `"Script error"` instead of containing useful information. This is a browser security measure intended to prevent passing data across domains that otherwise wouldn't be allowed to communicate. It's implemented in Firefox and Chrome.

To get the real error messages, do the following:

**1. Send the Access-Control-Allow-Origin header**

Setting the `Access-Control-Allow-Origin` header to `*` signifies that the resource can be accessed properly from any domain. You can replace `*` with your domain if necessary, for example `Access-Control-Allow-Origin: www.example.com`. However, handling multiple domains gets tricky, and may not be worth the effort if using a CDN due to caching issues that may arise. See more [here](http://stackoverflow.com/questions/1653308/access-control-allow-origin-multiple-origin-domains).

Here are some examples on how to set this header in various environments:

## Apache

In the folders where your JavaScript files will be served from, create an `.htaccess` file with the following contents:

`Header add Access-Control-Allow-Origin "*"`

## Nginx

Add the `add_header` directive to the location block that serves your JavaScript files:
```
location ~ ^/assets/ {
    add_header Access-Control-Allow-Origin *;
    ...
}
```

## HAProxy

Add the following to your asset backend where JavaScript files are served from:
```
rspadd Access-Control-Allow-Origin:\ *
```

## ExpressJS

Add the following to your app:

```js
app.use(function(req, res, next) {
  res.header("Access-Control-Allow-Origin", "*");
  res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
  next();
});
```

More examples for different platforms [here](http://enable-cors.org/server_expressjs.html)

## IIS

In IIS, you can use the following code in your `web.config`:

```
<location path="assets">
    <system.webServer>
        <httpProtocol>
            <customHeaders>
                <add name="Access-Control-Allow-Origin" value="*" />
            </customHeaders>
        </httpProtocol> 
    </system.webServer>
</location>
```

**2. Set crossorigin="anonymous" on the script tag**

In your HTML source, for each of the scripts that you've set the `access-control-allow-origin` header for, set `crossorigin="anonymous"` on the `SCRIPT` tag.

Make sure you verify that the header is being sent for the script file before adding the `crossorigin` property on the script tag. In Firefox, if the `crossorigin` attribute is present but the `Access-Control-Allow-Origin` header is not, the script won't be executed.

