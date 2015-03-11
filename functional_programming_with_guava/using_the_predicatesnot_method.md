# Using the Predicates.not method
`Predicates.not` 方法接受一个`Predicate`对象，并执行组成`Predicate`的逻辑非操作。
假设我们想要找出人口超过500,000的城市。不需要在写一个`Predicate`，我们可以在以存在的` PopulationPredicate`对象上使用` Predicate.not`：
```
Predicate largeCityPredicate = Predicate.not(smallPopulationPredicate);
```
