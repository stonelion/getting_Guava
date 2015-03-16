# Working with Collections
`Collections`是任何编程语言最核心的东西。不使用`collections`很难简单的写出一个有意义的程序。Guava库从`google-collections`开始就就有处理`collections`的经验。`Google Collections`库已经被废弃很长一段时间了，所有原始库的功能都合并到Guava中了。可以看看`com.google.common.collect`包下的类数量，得知使用`collections`的重要性；与Guava中其他包相比拥有最多的类。
本章中介绍如下的内容：
- 处理lists,maps和sets类上有用的静态方法。
- `Range`类，用于代表连续值集合边界。
- `Immutable`，不可变集合。
- `Bimaps`,可以从值到键的映射，同样也可以使用传统的键到值的映射。
- `Table`集合类型,是替代使用map的map场景有力的集合工具。
- `Multimaps`，可以用超过一个的值关联到唯一的key上。
- `FluentIterable`类,提供一系列处理`Iterable`实例有用的接口。
- `Ordering`类，增强我们处理`Comparators`的能力
