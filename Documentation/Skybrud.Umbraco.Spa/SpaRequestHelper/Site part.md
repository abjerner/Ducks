# Site part

When the `site` part is explicitly requested via the query string, or the `parts` parameter is left out, the `site` property in the JSON response will contain an object with information about the site being requested. The `SpaRequestHelper` class will look at both the `siteId` parameter in the query string and the host name of the request to determine the current site.

When a new SPA request is initialized in C#, the `InitArguments` method will be called to read and parse different information from the request - eg. query string parameters. It will also a bit of calculation based on the parsed parameters, such as looking up the root node of the current host name if the `siteId` parameter isn't specified.