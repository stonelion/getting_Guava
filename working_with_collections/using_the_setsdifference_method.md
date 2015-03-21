# Using the Sets.difference method
`Sets.difference`获取两个`set`实例作为参数，返回在第一个`set`中存在，但在第二个`set`中不存在元素的`SetView`。

`SetView`是`Sets`类中的静态内部类，表示给定`Set`实例不可修改的试图。任何在第二个集合中存在，但第一个集合中不存在的元素不会由这个试图表示。例如，下面的代码返回一个元素的`SetView`实例，"1":
```‵
    Set<String> s1 = Sets.newHashSet("1","2","3");
    Set<String> s2 = Sets.newHashSet("2","3","4");
    Sets.difference(s1,s2);
```
要是我们转换参数的顺序，返回的`SetView`实例也会只有一个元素,"4"。
