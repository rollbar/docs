# Filtering Javascript errors by language

If your application has an international user base, you may be receiving Javascript error reports in the local language of your users' browsers.

![](../images/filter-foreign-languages/error_spanish.png)

While Rollbar can't translate error messages into your preferred language, it is possible to group errors by language so that you have fewer items to manage.

Here are a few [custom grouping](/docs/custom-grouping/) recipes to match messages based on language:
## One supported language
The following rule groups errors where `client.language.javascript` does not contain `en-`:
```
  {
    "condition": {
      "ncontains": "en-", 
      "path": "client.javascript.language"
    }, 
    "fingerprint": "non-en error", 
    "title": "non-english error"
  }
```

## Multiple supported languages
The following rule groups errors where `client.language.javascript` does not contain `en-`,`fr-`,`de-`, or `es-`:
```
{
  "condition":{
    "all":[
      {"path":"client.javascript.language","ncontains":"en-"},
      {"path":"client.javascript.language","ncontains":"fr-"},
      {"path":"client.javascript.language","ncontains":"de-"},
      {"path":"client.javascript.language","ncontains":"es-"}
    ]
  },
  "fingerprint": "non-supported language error",
  "title": "non-supported language error"
}
```
