# CacheLoader
CacheLoaders是一个抽象类，因为load方法是抽象的。还有一个loadAll方法，这个方法需要Iterable对象，代理这个对象载入Iterable上包含的所有对象。
CacheLoader类上还有两个静态方法，可以使用到函数式编程的便利。
第一个方法是：
```
CacheLoader<Key,value> cacheLoader = CacheLoader.from(Function<Key,Value> func);
```
我们可以传进Function对象，转换输入对象达到另一个输出对象。CacheLoader实例会使用Function的输入对象作为key，输出结果作为值。

同样，我们还有另外一个方法。
```
CacheLoader<Object,Value> cacheLoader = CacheLoader.from(Supplier<Value> supplier);
```
上面的例子，我们使用Supplier实例建立CacheLoader。任何传递key给CacheLoader，都会调用Supplier.get()。还有一个规则假设，这些方法都会重用存在的Function或Supplier实例，并不会为建立CacheLoader构建新的对象。
