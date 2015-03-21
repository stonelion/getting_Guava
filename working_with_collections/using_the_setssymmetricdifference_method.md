# Using the Sets.symmetricDifference method
`Sets.symmetricDifference` 方法返回处于第一个或第二个集合中的元素，但不会包含两个集合中都存在的元素。返回的集合是一个不可修改的视图。使用之前的例子，则有：
```
Set<String> s1 = Sets.newHashSet("1","2","3");
Set<String> s2 = Sets.newHashSet("2","3","4");
Sets.SetView setView = Sets.symmetricDifference(s1,s2); //则会返回 [1,4]

```
