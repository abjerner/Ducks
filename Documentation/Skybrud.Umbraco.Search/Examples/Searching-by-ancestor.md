# Search by ancestor

For both content and media, Umbraco saves a field with the path of each content or media item. This field is a comma separated value (CSV) of the ancestors. CSV fields are not particular friendly for searching, but with the help of the `IndexCsv` extension method provided by this package, we can make them a lot friendlier.

## Make path searchable

The extension method is for an instance of `IndexingItemEventArgs`. So way we want to make the path of each item in the external index searchable, we could do as in the example below:

```csharp
using System;
using Examine;
using Examine.Providers;
using Umbraco.Core.Composing;
using Skybrud.Umbraco.Search.Extensions;

namespace UmbracoTests.Repositories.News {
    
    public class SearchComponent : IComponent {
        
        private readonly IExamineManager _examineManager;

        public SearchComponent(IExamineManager examineManager) {
            _examineManager = examineManager;
        }

        public void Initialize() {

            if (!_examineManager.TryGetIndex(Umbraco.Core.Constants.UmbracoIndexes.ExternalIndexName, out IIndex index))
                throw new InvalidOperationException($"No index found by name {Umbraco.Core.Constants.UmbracoIndexes.ExternalIndexName}");

            if (!(index is BaseIndexProvider indexProvider))
                throw new InvalidOperationException("Could not cast");
            
            indexProvider.TransformingIndexValues += IndexProviderOnTransformingIndexValues;

        }

        public void Terminate() {

            // do some cleanup

        }

        private void IndexProviderOnTransformingIndexValues(object sender, IndexingItemEventArgs e) {

            // THIS IS WHERE THINGS HAPPEN
            e.IndexCsv("path");

        }

    }

}
```

For using the method, you should specify the key if the field you wish to make searchable - eg. here the `path` field. The method will then split the value by the commas, and then join them back together using a space instead, and add the new value to a field named `path_search`.

## Search path

For a simple news search, we could create a `NewsSearchOptions` class implementing the `ISearchOptions` interface.

You can build up the Examine query your self, but you can also use the `QueryList` class from this package, as it provides some helpful methods - eg. the `AppendAncestor` method as used in the example below:

```csharp
using Skybrud.Umbraco.Search;
using Skybrud.Umbraco.Search.Options;

namespace UmbracoTests.Repositories.News {
    
    public class NewsSearchOptions : ISearchOptions {

        public int ContextId { get; set; }
        
        public string GetRawQuery(ISearchHelper searchHelper) {

            QueryList list = new QueryList();

            if (ContextId > 0) list.AppendAncestor(ContextId);

            list.AppendNodeTypeAlias("newsPage");

            return list.GetRawQuery();

        }

    }

}
```

In case you wish to search by multiple ancestors, there is a `AppendAncestors` method as well, which will result in an OR based search for the specified ancestors.