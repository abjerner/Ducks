# Sorting results

When searching in Examine, the results you getting back from the search are sorted by their relevance by default.

If you need them returned sorted by something else, you should ideally handle the sorting at the Examine/Lucene level for the best performance. But in some cases, you may need to sort by more complex fields, or by values from multiple fields.

For this purpose, your options class can implement the [IPostSortOptions](https://github.com/skybrud/Skybrud.Umbraco.Search/blob/master/src/Skybrud.Umbraco.Search/Options/Sorting/IPostSortOptions.cs) interface. The *post* part in the name suggests that the sorting is done *post search* (after the results have been returned from Examine).

The interface describes a single `Sort` method, both taking and returning an instance of `IEnumerable<ISearchResult>` containing the results from the search. For a member search, you might want to sort the members by their name:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Examine;
using Skybrud.Umbraco.Search;
using Skybrud.Umbraco.Search.Options;
using Skybrud.Umbraco.Search.Options.Sorting;
using Umbraco.Core;

namespace UmbracoEightThirteen.Repositories.News {
    
    public class MemberSearchOptions : MySearchOptionsBase, IGetSearcherOptions, IPostSortOptions {

        public ISearcher GetSearcher(IExamineManager examineManager, ISearchHelper searchHelper) {
            examineManager.TryGetIndex(Constants.UmbracoIndexes.MembersIndexName, out IIndex index);
            return index?.GetSearcher() ?? throw new Exception("Oh noes!");
        }

        public IEnumerable<ISearchResult> Sort(IEnumerable<ISearchResult> results) {
            return results.OrderBy(x => x.GetValues("nodeName")?.FirstOrDefault());
        }

    }

}
```

Other examples may include:

- [Sorting by a date](../../examples/sorting-by-a-date/)