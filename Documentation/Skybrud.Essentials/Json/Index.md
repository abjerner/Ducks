---
icon: fa-code
title: JSON
---

# JSON

## JsonUtils

In Skybrud.Essentials, the static `JsonUtils` class comes with a number of helpful utility methods and other functionality for working with JSON (and [JSON.net](https://www.newtonsoft.com/json) in particular). 

For instance, you can parse or load JSON objects using the `JsonUtils.ParseJsonObject` and `JsonUtils.LoadJsonObject` methods respectively:

```c#
@using Skybrud.Essentials.Json
@{

    // Parse a JSON object from a string
    JObject json1 = JsonUtils.Parse("{\"hello\":\"world\"}");
    
    // Load a JSON object from a file on disk
    JObject json2 = JsonUtils.Load("C:/path/to/file.json");

}
```

The `JsonUtils.Parse` method does somewhat the same as `JObject.Parse`, but JSON.net's default settings will deserialize string properties that look like dates to actual instances of `DateTime` - which when serialized back to a JSON string might not look like the original string value. The `JsonUtils.Parse` will make sure that these values will stay as strings so the format wont change.

The `JsonUtils.Load` will read from the file so you don't have to do this your self. The contents of the file is then passed on to the `JsonUtils.Parse` method, giving the same result as described above.

## Converters

Skybrud.Essentials also comes with a number of JSON converters. For instance, there are a number of ways to serialize an enum value. Default in JSON.net is to use the enum values numeric value, but this may not always be the desired result.

So, if you wish to store your enum values using camel case (eg. `camelCase`), you can use the `EnumCamelCaseConverter` on your property or enum class. In a similar way, you can convert to Pascal case (eg. `PascalCase`) using `EnumPascalCaseConverter`, and to lower case (eg. `lowercase`) using `EnumLowerCaseConverter`.