# Lists
`Lists`是处理`List`实例的工具类。他最大的便利是提供建立新`List`实例的能力:
```
List<Person> personList = Lists.newArrayList();
```


##Using the Lists.partition method
`Lists.partition()`方法是一个有趣的方法，这个方法从给定`list`上返回大小为 `n` 的子列表。例如，假设之前已经建立了四个`Person`对象，然后使用如下的`Lists`类的静态工厂方法构造出一个`List`:
```
List<Person> personList =
Lists.newArrayList(person1,person2,person3,person4);
```
然后我们调用`Lists.partition()`方法，指定划分成2个分片：
```
List<List<Person>> subList = Lists.partition(personList,2);
```
这个例子中，`subList`列表可能包含`[[person1,person2],[person3,person4]] `.
`partition`方法返回连续的有相同大小的子列表，但最后一个列表可能不一样，可能会更小。例如，如果我们将3作为大小传递给`sublist`方法，`Lists.partition()` 可能会返回 `[[person1,person2,person3],[person4]]`。
