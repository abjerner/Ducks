# Base classes

Instead of implementing the `ISearchOptions` interface from scratch each time, it's recommended to use a base class so you'd have a bit of logic to start with. For instance this package provides the [SearchOptionsBase](https://github.com/skybrud/Skybrud.Umbraco.Search/blob/master/src/Skybrud.Umbraco.Search/Options/SearchOptionsBase.cs) that you could extend, and then override the logic that you'd need to adjust.

## SearchOptionsBase

See the [SearchOptionsBase](https://github.com/skybrud/Skybrud.Umbraco.Search/blob/master/src/Skybrud.Umbraco.Search/Options/SearchOptionsBase.cs) class on GitHub.

## Custom base class

When working on client solution, we'd usually create a custom base class for that particular solution. For instance:

```csharp
using System;
using System.Text.RegularExpressions;
using Skybrud.Umbraco.Search;
using Skybrud.Umbraco.Search.Options;
using Skybrud.Umbraco.Search.Options.Fields;

namespace Umbracotests.Repositories.Search {
    
    public class MySearchOptionsBase : ISearchOptions {

        /// <summary>
        /// Gets or sets the context (ID of ancestor) under which to search.
        /// </summary>
        public int ContextId { get; set; }

        /// <summary>
        /// Gets or sets the text to search for.
        /// </summary>
        public string Text { get; set; }

        /// <summary>
        /// Gets or sets whether the check on the <c>hideFromSearch</c> field should be disabled.
        /// </summary>
        public bool DisableHideFromSearch { get; set; }

        public virtual string GetRawQuery(ISearchHelper searchHelper) {
            return GetQueryList(searchHelper).GetRawQuery();
        }

        protected virtual QueryList GetQueryList(ISearchHelper searchHelper) {

            QueryList query = new QueryList();

            SearchType(searchHelper, query);
            SearchText(searchHelper, query);
            SearchPath(searchHelper, query);
            SearchHideFromSearch(searchHelper, query);

            return query;

        }

        protected virtual FieldList GetTextFields(ISearchHelper helper) {
            return new FieldList {
                new Field("nodeName", 50),
                new Field("title", 40),
                new Field("teaser", 20)
            };
        }

        protected virtual void SearchType(ISearchHelper searchHelper, QueryList query) { }

        protected virtual void SearchText(ISearchHelper searchHelper, QueryList query) {

            if (string.IsNullOrWhiteSpace(Text)) return;

            string text = Regex.Replace(Text, @"[^\wæøåÆØÅ\-@\. ]", string.Empty).ToLowerInvariant().Trim();

            string[] terms = text.Split(new[] { ' ' }, StringSplitOptions.RemoveEmptyEntries);
            if (terms.Length == 0) return;

            // Fallback if no fields are added
            FieldList fields = GetTextFields(searchHelper);
            if (fields == null || fields.Count == 0) fields = FieldList.GetFromStringArray(new[] { "nodeName", "title", "teaser" });

            query.Add(fields.GetQuery(terms));

        }

        protected virtual void SearchPath(ISearchHelper searchHelper, QueryList query) {
            if (ContextId > 0) query.AppendAncestor(ContextId);
        }

        protected virtual void SearchHideFromSearch(ISearchHelper searchHelper, QueryList query) {
            if (DisableHideFromSearch) return;
            query.Add("hideFromSearch:0");
        }

    }

}
```

The only thing coming from the `ISearchOptions` interface is the `GetRawQuery` method. The other methods are extension points, each with a default implementation that you may or may not choose to overwrite in each class extending your custom base class.

### GetQueryList

The `GetQueryList` splits the construction of the query into different methods, which makes it easier to override the different parts. You may even choose to override this method in a sub class - eg. if you have a need beyond the methods of the base class:

```csharp
protected override QueryList GetQueryList(ISearchHelper helper) {

    QueryList query = base.GetQueryList(helper);

    query.Add("tags:umbraco");

    return query;

}
```

### GetTextFields

This method describes the default fields that should be used for the free text search. Which fields to search may be determined by other properties, which is why this has been delegated to it's own method.

For instance for a grid based page, you could override it to include the grid content as well:

```csharp
protected override FieldList GetTextFields(ISearchHelper helper) {
    return new FieldList {
        new Field("nodeName", 50),
        new Field("title", 40),
        new Field("teaser", 20),
        new Field("grid", 5)
    };
}
```

or call the base method to inherit the default fields:

```csharp
protected override FieldList GetTextFields(ISearchHelper helper) {
    
    var fields = base.GetTextFields(helper);

    fields.Add("grid", 5);

    return fields;

}
```

The second parameter is the boost for the particular field. A third parameter also let's you specify a fuzzy level.

### SearchType

The base class in this example doesn't restrict the search to any specific types by default. But a news search, you could override the `SearchType` method do something like:

```csharp
protected override void SearchType(ISearchHelper searchHelper, QueryList query) {
    
    query.AppendNodeTypeAlias("newsPage");

}
```

### SearchText

When first implemented in the base class, you may not need to override the `SearchText`, as the fields it's searching is controlled by the `GetTextFields` method. But should you have the need, you can override this one as well.

### SearchPath

If specified via the `ContextId` property, this method restricts the search to items under a given ancestor.

### SearchHideFromSearch

We typically add a `hideFromSearch` property to pages in Umbraco, so the editors can exclude individual pages from the search if they need to. This method makes sure that this criteria is met, but also let's you disable this behavior via the `DisableHideFromSearch`.