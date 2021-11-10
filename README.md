# treatise-on-dotnet-collections
A summary of my thoughts on .NET collections. Probably also an opinionated guide on how to use them.


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
- Immutable collection interfaces
  - `IImmutableDictionary`, `IImmutableList` etc.
- Thread-safe collections
  - For concurrency
  - `ConcurrentBag`, `ConcurrentDictionary` etc.
- Non-generic collections
- Those things from `ObjectModel` namespace
  - `ReadOnlyCollection` etc.

## Examples

`IReadOnly.*` interfaces don't expose writable methods, but that alone doesn't guarantee immutability. One who has access to the collection's internals can still modify it:

```c#
void Main()
{
	var coll = new List<string>(){"a", "b", "c"};
	Action foo = () => { coll.Add("q"); };
	DoThings(coll, foo);
}

void DoThings(IReadOnlyCollection<string> coll, Action callback)
{
	for (int i=0; i<3; ++i){
		var text = string.Join(", ", coll);
		Console.WriteLine(text);
		callback.Invoke();
	}
}
```

Result:
```
a, b, c
a, b, c, q
a, b, c, q, q
```
