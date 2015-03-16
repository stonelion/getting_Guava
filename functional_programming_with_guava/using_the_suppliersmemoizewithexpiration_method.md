# Using the Suppliers.memoizeWithExpiration method
`Suppliers.memoizeWithExpiration` 方法与`memoize`方法以相同的方式工作，但是在给定时间之后会死亡。当调用`get`时，包装`Supplier`对象从代理`Supplier`对象上取得实例。之后，包装`Supplier`对象缓存实例一段给定的时间。要注意到实例并不是在物理缓存中持有；而是包装`Supplier`对象持有一个实例变量，这个变量由代理的`Supplier`对象设置并返回。看下例子：
```
Supplier<Predicate<String>> wrapped =
Suppliers.memoize(composedPredicateSupplier,10L,TimeUnit.MINUTES);
```
再次包装`Supplier`，并设置超时时间为`10`分钟。对于`ComposedPredicateSupplier而言并没有什么变化，但`Supplier`返回的对象可能有改变，例如从数据库中获取数据，这时`memoizeWithExpiration`方法会十分有用。

