# ArrayListMultimap
`ArrayListMulitmap`是一个使用`ArrayList`存储给定key
 value的map。建立`ArrayListMultimap`实例，我们使用如下的方法：
```
- ArrayListMultimap<String,String> multiMap = ArrayListMultimap.create();
- ArrayListMutilmap<String,String> multiMap = ArrayListMultimap.create(numExcpectedKeys,numExpectedValuesPerKey);
- ArrayListMulitmap<String,String> mulitMap = ArrayListMultimap.create(listMultiMap);
```

第一个方法只是简单地创建一个默认大小key和`ArrayList`空的`ArrayListMultimap`。
第二个方法设置key的初始大小和`ArrayList`持有对象的大小。
最后一个方法使用所提供的`Multimap`参数创建一个新的`ArrayListMultimap`实例。
让我们用下面的例子来阐述下如何使用`ArrayListMultimap`:

```
@Test
public void testArrayListMultiMap(){
    ArrayListMultimap<String,String> multiMap =
ArrayListMultimap.create();
    multiMap.put("Foo","1");
    multiMap.put("Foo","2");
    multiMap.put("Foo","3");
    List<String> expected = Lists.newArrayList("1","2","3");
    assertEquals(multiMap.get("Foo"),expected);
}
```
现在，让我们考虑另一个使用场景。如果我们多次添加相同的key-value对，会发生什么？看看下面的单元测试，并思考下时候会通过。
```
@Test
public void testArrayListMultimapSameKeyValue(){
    ArrayListMultimap<String,String> multiMap = ArrayListMultimap.create();
    multiMap.put("Bar","1");
    multiMap.put("Bar","2");
    multiMap.put("Bar","3");
    multiMap.put("Bar","3");
    multiMap.put("Bar","3");
    List<String> expected = Lists.newArrayList("1","2","3","3","3");
    assertEquals(multiMap.get("Bar"),expected);
}
```
因为一个List并不强制他所有元素都是唯一的，所以上面的单元测试会通过。我们仅仅只是添加另一个元素到List所关联的key中。
一个小测验，看看下面的代码：

```
multiMap.put("Foo","1");
multiMap.put("Foo","2");
multiMap.put("Foo","3");
multiMap.put("Bar","1");
multiMap.put("Bar","2");
multiMap.put("Bar","3");
```

`multimap.size()`调用的结果是什么？6，还是2？`size()`调用是计算所有的在每个List中找到的value，而并不是map中所有List实例的个数。此外，`values()`方法返回包含所有六个值的集合，而不是两个只有三个元素的list。虽然这乍看之下有点奇怪，我们需要记住的是`multimap`并不是一个真正的map。但，如果我们需要典型的map行为，我们可以这么做：

```
Map<String,Collection<String>> map = multiMap.asMap();
```

调用`asMap()`返回原始multimap中每个key所关联集合的map。所返回的map是一个活的试图，对试图的改变会反映给底层的multimap。当然，需要记住返回的map不支持`put(key,value)`方法。我们花费了众多时间谈论`ArrayListMultimap`，当还有另外一个multimap实现。
