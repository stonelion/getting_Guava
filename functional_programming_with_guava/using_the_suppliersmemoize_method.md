#Using the Suppliers.memoize method
`Suppliers.memoize` 方法返回一个所提供的`Supplier`实例的代理实例。代理实例建立并返回包装的`Supplier`对象。在返回对象给调用者之前，包装的`Supplier`实例缓存的这个对象。 所有之后的调用`get`方法都会返回缓存的实例。

现在看看`Suppliers.memoize`如何使用:

```
Supplier<Predicate<String>> wrapped =
Suppliers.memoize(composedPredicateSupplier);
```
仅仅通过添加一行，则可以在每次调用`Supplier`对象，返回相同的`Predicate`对象实例。
