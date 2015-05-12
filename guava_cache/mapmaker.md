# MapMaker
MapMaker类使用fluent接口API，允许我们可以快速的构造ConcurrentHashMap。
让我们看例子：

```
    ConcurrentMap<String,Book> books = new MapMaker()
    .concurrencyLevel(2)
    .softValues()
    .makeMap();
```
到这里，我们建立ConcurrentMap使用string作为key，book作为value。concurrencyLevel()，设置我们期望map中并发修改的级别。我们同样指定softValues()方法，所以从map中取到的value是包裹到SoftReference对象中，并且可能被垃圾收集器收集的。其他我们可以使用的操作包括weakKeys()和weakValues()，但是，并没有选项来使用softKeys()。对key或者value使用WeakReferences或SoftReferences的时候，如果存在垃圾收集，全部的entry会从map中删除。部分的entry则不会暴露给客户端。
