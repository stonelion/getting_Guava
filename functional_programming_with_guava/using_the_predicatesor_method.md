# Using the Predicates.or method
`Predicates.or`方法接受多个`Predicate`实例，返回一个当所有组成的`Predicate`实例任意一个算为`true`时，也返回`true`的`Predicate`实例。 (与逻辑或相一致)。一旦某个组合的`Predicate`实例返回`true`，则再不会计算。例如，假定我们需要找出人口小于或等于500，000，或者有温度极限的城市：
```
Predicate smallTemperate =
Predicates.or(smallPopulationPredicate,temperateClimatePredicate);
```

还有可选的调用`Predicates.or`方式，签名如下：
```
Predicates.or(Iterable<Predicate<T>> predicates);
Predicates.or(Predicate<T> ...predicates);
```
