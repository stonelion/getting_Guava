# Using the Maps.asMap method
虽然`Maps.uniqueIndex`方法使用`Function`从给定值上产生key。`Maps.asMap`方法则执行相反的操作。`Maps.asMap`方法使用一个对象集合作为key，`Function`则在每个key对象上生成value。还有另外一个方法`Maps.toMap`，使用同样的参数，但是会返回`ImmutableMap`而不是map视图。他们之间最主要的不同就是，`Maps.asMap`方法返回的map会映射所有得改变到源map上，而`Maps.toMap`所返回的并不会对源map进行修改。
