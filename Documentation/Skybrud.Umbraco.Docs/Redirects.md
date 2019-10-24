# Redirects





### Handling redirects

When editors are moving or renaming content in Umbraco, Umbraco will automatically keep track of this so the old URL of a page will point to the new URL.

The SPA package also has a dependency for our [**Skybrud.Umbraco.Redirects**](https://github.com/skybrud/Skybrud.Umbraco.Redirects) package, which lets editors create manual redirects to content, media and even external URLs. The `SpaControllerBase` class has build in support for both types of redirects.

You can also do other types of redirects - eg. by overriding either the `PreContentLookup` or `PostContentLookup` methods:

```csharp
protected override void PostContentLookup(SpaRequest request) {

    // Skip if we don't have a content item
    if (request.Content == null) return;

    // If "content" matches the culture node, we get the content of the front page instead
    if (request.Content.ContentType.Alias == ClientNameConstants.DocumentTypes.Culture) {
        request.Content = request.Content.FirstChild(ClientNameConstants.DocumentTypes.FrontPage) ?? request.Content;
    }

}
```

Four our sites, we typically have a culture node directly below the site node, which is used for storing settings for a specific culture on the site. The culture node doesn't have any contents of it's own, so we use the `PostContentLookup` method to redirect the culture node to the front page of the culture.



### Returning a redirect

At the time of writing, the `SpaControllerBase` class contains three different overloads of the ` ReturnRedirect ` method. The methods are responsible for returning information about a redirect which the frontend is then able to understand and process.

The methods are defined as following:

```csharp
protected virtual HttpResponseMessage ReturnRedirect(SpaRequest request, string destinationUrl)
```

```csharp
protected virtual HttpResponseMessage ReturnRedirect(SpaRequest request, string destinationUrl, bool permanent)
```

```csharp
protected virtual HttpResponseMessage ReturnRedirect(SpaRequest request, string destinationUrl, HttpStatusCode statusCode)
```

The first two methods uses the third method, so if you need to override any of the logic, it may be best to override the last method.

#### I'm a teapot

A combination of older browsers and older operating systems have problems with understanding the typical HTTP status code for redirects when the request is made as an AJAX request.

As a way to handle this, the `GetData` endpoint will return a response with a 418 status code (called [I'm a teapot]( https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/418 )) when the client should redirect the user to another page than the one originally requested. 418 was introduced as an April Fools' joke, but it's an error code supported by all major browsers - old and new.

The response body will instead expose the actual status code - eg. as shown here:

```json
{
  "meta": {
    "code": 307,
    "error": "Page has moved"
  },
  "data": {
    "url": "/my-destination-page/",
  }
}
```

If the frontend is server side rendered, the browser should receive the status code as specified by the `meta.code` property.
