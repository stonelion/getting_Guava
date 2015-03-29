# HashMultimap
`HashMultimap`是基于hash table。与`ArrayListMultimap`不同，多次插入相同的key-value对是不支持的。让我们看看如下的例子：
```
    HashMultimap<String,String> multiMap = HashMultimap.create();
    multiMap.put("Bar","1");
    multiMap.put("Bar","2");
    multiMap.put("Bar","3");
    multiMap.put("Bar","3");
    multiMap.put("Bar","3");
```
这个例子中，用`Bar`这个key插入相同的值三次。当我们调用`multiMap.size()`，则会放回3，只有不同的key-value对才会保留下来。除了不支持重复key-value插入外，其他的功能完全是我们所需要的。
Before we move on, it's worth mentioning some of the other implementations
of multimap. First, there are three immutable implementations:
ImmutableListMultimap, ImmutableMultimap, and ImmutableSetMultimap.
There is LinkedHashMultimap, which returns collections for a given key that have
the values in the same order as they were inserted. Finally, we have TreeMultimap
that keeps the keys and values sorted by their natural order or the order specified by
a comparator.
