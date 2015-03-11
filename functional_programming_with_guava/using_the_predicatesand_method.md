# Using the Predicates.and method
`Predicates.and`方法接受多个`Predicate`实例，返回一个当所有组成的`Predicate`都计算为`true`时，才返回`true`的`Predicate`。 (与逻辑与相一致)。只要有一个组成的`Predicate`返回false，则其他的`Predicate`实例计算会停止。

例如，我们只想要人口低于500,000，并且平均降雨量不超过45.7英寸每年的城市。：
```
Predicate smallAndDry =
    Predicates.and(smallPopulationPredicate,lowRainFallPredicate);
```
还有可选的调用`Predicates.and`方式，签名如下：
```
Predicates.and(Iterable<Predicate<T>> predicates);
Predicates.and(Predicate<T> ...predicates);
```
