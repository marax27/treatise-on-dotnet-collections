# treatise-on-dotnet-collections
A summary of my thoughts on .NET collections. Probably also an opinionated guide on how to use them.

## Critical background reading
- https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/guidelines-for-collections

## Summary

### Regular collections
- Concrete implementations
  - General purpose: `List`, `HashSet`, `Dictionary` etc.
  - Special purpose: `Stack`, `Queue`, `LinkedList` etc.
- Read-write collection interfaces
  - `IList`, `ISet`, `ICollection` etc.
- Read-only collection interfaces
  - `IReadOnlyCollection`, `IReadOnlyList`, `IReadOnlyDictionary` etc.
- Enumerations
  - `IEnumerable`, which is pretty much a wrapper on `IEnumerator`.

### Immutable collections
- Implementations
  - `ImmutableDictionary`, `ImmutableArray` etc.
- Interfaces
  - `IImmutableDictionary`, `IImmutableList` etc.

### Thread-safe collections
- Implementations
  - `ConcurrentBag`, `ConcurrentDictionary`, `ConcurrentQueue`, `ConcurrentStack` etc.
- Interfaces
  - `IProducerConsumerCollection` (?)

### Extras
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

In order to achieve true immutability, one needs the `I?Immutable.*` collections.

