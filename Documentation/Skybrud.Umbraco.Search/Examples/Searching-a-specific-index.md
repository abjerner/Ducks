# Searching a specific index

By default this package will search in Umbraco's external index. To search in another index, the package provides two different approaches:

## ISearcherOptions interface

By making your options class also implementing the [ISearcherOptions](https://github.com/skybrud/Skybrud.Umbraco.Search/blob/master/src/Skybrud.Umbraco.Search/Options/ISearcherOptions.cs) interface, it requires you to add the `Searcher` property.

With this property, you can return the desired index to be searched. You could set the property from the constructor of your options class:

```csharp
using Examine;
using Skybrud.Umbraco.Search;
using Skybrud.Umbraco.Search.Options;
using Umbraco.Core;

namespace UmbracoTests.Repositories.Members {
    
    public class MemberSearchOptions : MySearchOptionsBase, ISearcherOptions {

        public ISearcher Searcher { get; }

        public MemberSearchOptions() {
            if (ExamineManager.Instance.TryGetIndex(Constants.UmbracoIndexes.MembersIndexName, out IIndex index)) {
                Searcher = index.GetSearcher();
            }
        }

    }

}
```

If you concrete class also implements a setter for this property, you'll be able to set the searcher from the context in which you're using your options class.

## IGetSearcherOptions

Generally we strive to isolate as much logic inside the options class as possible, so you don't need to know about the inner workings of the search when using your options class around your solution.

To make this possible, you can therefore implement the [IGetSearcherOptions](https://github.com/skybrud/Skybrud.Umbraco.Search/blob/master/src/Skybrud.Umbraco.Search/Options/IGetSearcherOptions.cs) interface instead.

Opposed to the `Searcher` property described earlier on this page, this interface instead describes a `GetSearcher` method, which is then automatically called when this package performs the search for you.

```csharp
using Examine;
using Skybrud.Umbraco.Search;
using Skybrud.Umbraco.Search.Options;
using Umbraco.Core;

namespace UmbracoTests.Repositories.Members {
    
    public class MemberSearchOptions : MySearchOptionsBase, ISearcherOptions {

        public ISearcher GetSearcher(IExamineManager examineManager, ISearchHelper searchHelper) {
            examineManager.TryGetIndex(Constants.UmbracoIndexes.MembersIndexName, out IIndex index);
            return index?.GetSearcher() ?? throw new Exception("Oh noes!");
        }

    }

}
```

This way the `IExamineManager` is also passed along as a parameter instead of being accessed via the static `ExamineManager.Instance` property.