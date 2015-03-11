# Using the Predicates class
`Predicates`类包含许多处理`Predicates`实例有用的方法。`Predicates`类提供了许多有用的方法，处理`Boolean`条件，使用`and`或`or`串联`Predicate`实例，提供`not`来取反给定的`Predicate`所得出的值。
同样提供了`Predicates.compose`方法，但是，这个方法使用`Predicate`实例和`Function`对象，返回对`Function`输出的计算结果。

首先,让我们先假定有如下两个`Predicates`类实例定义，和之前的`PopulationPredicate`定义：

```
public class TemperateClimatePredicate implements Predicate<City> {
    @Override
    public boolean apply(City input) {
        return input.getClimate().equals(Climate.TEMPERATE);
    }
}

public class LowRainfallPredicate implements Predicate<City> {
    @Override
    public boolean apply(City input) {
        return input.getAverageRainfall() < 45.7;
    }
}
```

再次说明，并不必须的，我们一般使用匿名类定义`Predicate`实例。
