# BiMap
从value导航到map中的key。`bimap`就是做这样的功能。
`bimap`是唯一的，就是保持map中的value是唯一的。这也是倒置map和从value到key导航的首要条件。给bimap插入值操作十分不同。.
让我们先看看一个例子：
```
BiMap<String,String> biMap = HashBiMap.create();
biMap.put("1","Tom");
//这个调用会抛出 IllegalArgumentException 异常!
biMap.put("2","Tom");
```
这个例子中，我们添加相同值而不同的key，传统的map就是这么做的。但是使用`bimap`,插入一个在map中已经存在value的新key，则会抛出`IllegalArgumentException`异常。
