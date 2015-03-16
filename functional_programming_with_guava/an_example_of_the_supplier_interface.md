# An example of the Supplier interface
下面的代码是使用`Supplier`接口的例子：
```
public class ComposedPredicateSupplier implements Supplier<Predicate<String>> {
@Override
    public Predicate<String> get() {
        City city = new City("Austin,TX","12345",250000, Climate.SUB_TROPICAL,45.3);
        State state = new State("Texas","TX", Sets.newHashSet(city),Region.SOUTHWEST);
        City city1 = new City("New York,NY","12345",2000000,Climate.TEMPERATE,48.7);
        State state1 = new State("New York","NY",Sets.newHashSet(city1),Region.NORTHEAST);
        Map<String,State> stateMap = Maps.newHashMap();
        stateMap.put(state.getCode(),state);
        stateMap.put(state1.getCode(),state1);
        Function<String,State> mf = Functions.forMap(stateMap);
        return Predicates.compose(new RegionPredicate(), mf);
}
}
```
这个例子中，可以看到，我们使用`Functions.forMap`建立`Function`实例，用于通过使用缩写来查询美国中的州。然后，我们使用`Predicate`实例，计算出国家中的哪个州符合要求。最后，使用`Function`和`Predicate`实例作为参数给`Predicates.compose`方法，这个方法的结果会调用`get`方法。这里我们也使用了两个静态工厂方法，`Maps.newHashMap()`和`Set.newHashSet()`,这些方法都是Guava的工具类，可以在`com.google.common.collect`包中找到。注意到，我们在这里选择的是每次都返回一个新的实例。也可以很容易的在`ComposedPredicateSuplier`类的构造器中做完所有的工作，也在每次调用的时候放回相同的实例，但是，看看后面的介绍，Guava提供了更简单的选择。
