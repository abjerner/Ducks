# SpaRequestHelper

Most of the logic for handling a SPA request is delegated to the `SpaRequestHelper` class, so the WebAPI controller itself can be quite minimal:

```csharp
using System.Web.Http;
using Skybrud.Umbraco.Spa.Attributes;
using Skybrud.Umbraco.Spa.Models;
using Skybrud.WebApi.Json;
using Umbraco.Web.WebApi;

namespace CustomerName.Controllers.Api.Spa {

    [JsonOnlyConfiguration]
    [AccessControlAllowOrigin]
    public class SpaController : UmbracoApiController {

        [HttpGet]
        [HttpOptions]
        public object GetData() {

            // Initialize a new request
            SpaRequest request = new SpaRequest();

            // Iniitialize a new helper
            SpaRequestHelper helper = new SpaRequestHelper();

            // Get and return the response
            return helper.GetResponse(request);

        }

    }

}
```

The `SpaRequestHelper` class doesn't know much about your sites and pages by default, but it contains a long list of extension points that can be tailored to fit your needs.

By creating your own class that inherits from `SpaRequestHelper`, you can override most of it's methods. As part of the JSON response is an object with some information about the site being requested. By default this data will be based on an instance of `SpaSiteModel`. This class will however only have some basic information about your site, so to tailor this part, you can provide an instance of your own class instead - eg. as shown here:


```csharp
public class ClientSpaRequestHelper : SpoaRequestHelper {

    protected override void InitSiteModel(SpaRequest request) {
        if (request.Site == null) return;
        request.SiteModel = new ClientSiteModel(request.Site, request.Culture);
    }

}
```