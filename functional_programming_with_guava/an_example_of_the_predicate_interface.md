# An example of the Predicate interface
一个简单的使用`Predicate`接口的例子，这个例子会使用之前例子中的`City`类。这里，我们定义一个`Predicate`用于决定是否某个城市小于最小人口：

```
public class PopulationPredicate implements Predicate<City> {
    @Override
    public boolean apply(City input) {
        return input.getPopulation() <= 500000;
    }
}
```
简单的检查`City`对象的`population`成员属性，并在人口数小于或等于500000时返回`true`。一般情况下，`Predicate`接口被匿名类实现，并且作为获取集合中元素的过滤条件。由于`Predicate`和`Function`接口类似，之前介绍到也同样可以应用到`Predicate`上。
