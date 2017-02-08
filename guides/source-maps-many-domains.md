If you'd like to use source maps with the same code that is deployed on many domains, use the following code (changing `yourdomainhere` to your domain in the `locRegex` variable):

```javascript
var _rollbarConfig = {
  // ...
  transform: function(payload) {
    var trace = payload.data.body.trace;
    var locRegex = /^(https?):\/\/[a-zA-Z0-9.-_]+\.yourdomainhere\.com(.*)/;
    if (trace && trace.frames) {
      for (var i = 0; i < trace.frames.length; i++) {
        var filename = trace.frames[i].filename;
        if (filename) {
          var m = filename.match(locRegex);
          trace.frames[i].filename = m[1] + 'dynamichost' + m[2];          
        }
      }
    }
  }
}

```