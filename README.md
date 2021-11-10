# treatise-on-dotnet-collections
A summary of my thoughts on .NET collections


## Summary

- Regular collections
  - Concrete implementations
  - `List`, `HashSet` etc.
- Enumerations
  - `IEnumerable`, which is basically a wrapper on `IEnumerator`
- Read-write collection interfaces
  - `IList`, `ISet`, `ICollection` etc.
- Read-only collection interfaces
  - `IReadOnlyCollection`, `IReadOnlyList`, `IReadOnlyDictionary` etc.
- Immutable collections
  - `ImmutableDictionary`, `ImmutableArray` etc.
- Thread-safe collections
  - For concurrency
  - `ConcurrentBag`, `ConcurrentDictionary` etc.
- Non-generic collections
