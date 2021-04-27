# Skybrud.Umbraco.Search

The package revolves around the `ISearchHelper` and the `ISearchOptions` interfaces, where both can be used to create complex Examine searches.

The `ISearchHelper` interface is your resource for searching making searches in Examine, while instances of the `ISearchOptions` interface can be used to describe what to search for.



## Accessing an instance

You an get an instance of `ISearchHelper` via dependency injection - such as:

```csharp
public class SearchController : UmbracoApiController {
    
    private readonly ISearchHelper _searchHelper;
    
    public SearchController(ISearchHelper searchHelper) {
        _searchHelper = searchHelper;
    }
    
}
```

Or directly from the DI container:

```csharp
ISearchHelper searchHelper = Current.Factory.GetInstance<ISearchHelper>();
```

## Performing a search

The `ISearchHelper` interfaces describes a `Search` method taking an instance of `ISearchOptions`, where a concrete implementation of the interface may be used to control the search.

Examples of such concrete implementations are the `SearchOptionsBase` and `OffsetSearchOptionsBase` classes which are also a part of this package.

The `ISearchOptions` interface describes a `GetRawQuery` method for returning the raw Examine query. The idea is that the you can have various classes implementing the interface, each with properties related to a given area, and each property determining how to search in Examine. For instance, you might have a site where you'd want to search news articles, so you'd have a `NewsSearchOptions` class:

```csharp
public class NewsSearchOptions : ISearchOptions {

    public int ContextId { get; set; }

    public string Text { get; set; }

    public string GetRawQuery(ISearchHelper searchHelper) {

        QueryList query = new QueryList();

        if (ContextId > 0) query.Add($"path_search:{ContextId}");

        query.AppendNodeTypeAlias("newsPage");

        // TODO: search for "Text"

        return query.GetRawQuery();

    }

}
```

With this example, the `NewsSearchOptions` class specifies a `ContextId` property, as well as a `Text` property. The context ID could be used if you have more than one news archive, but wish to limit the results of the search to a one specific news archive. Notice that [the path of content or media items in Examine is not searchable by default](#). The text property may be used to do a free text search across multiple fields on each node in the index.

The `GetRawQuery` method then puts the Examine query together. Both for based on the properties of the options class, but also hardcoded constants like limiting the search to content items of the type `newsPage`.