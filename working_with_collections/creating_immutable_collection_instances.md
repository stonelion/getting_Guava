# Creating immutable collection instances
因为与可变集合的功能是完全相反的，这里阐述主要的不同。所有Guava不可变集合都有一个静态嵌套的Builder类，这个类使用fluent接口方式来建立需要的实例。下面使用ImmutableListMultimap.Builder作为例子：

```
MultiMap<Integer,String> map = new ImmutableListMultimap.Builder<Integer,String>().put(1,"Foo").putAll(2,"Foo","Bar","Baz").putAll(4,"Huey","Duey","Luey").put(3,"Single").build();
```
