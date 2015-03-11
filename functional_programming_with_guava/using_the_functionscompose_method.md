# Using the Functions.compose method
现在，假设另外一个代表城市的类，如下：
```
public class City {
    private String name;
    private String zipCode;
    private int population;

    public String toString() {
        return name;
    }
}
```
考虑下这样的场景：你想要建立一个`Function`实例，输入`State`对象，把这个转换成以逗号隔开的这个州中的主要城市的字符串。

`Function`对象看起来如下：
```
public class StateToCityString implements Function<State,String>
    @Override
    public String apply(State input) {
        return Joiner.on(",").join(input.getMainCities());
    }
}
```
现在，让我们更进一步。你想要当个`Function`实例，输入州的缩写，然后返回以逗号隔开的州主要城市字符串。Guava为这种场景提供了一个非常好的解决方案。就是`Functions.compose`方法，该方法需要两个`Function`实例作为参数，然后返回一个组合这两个实例的`Function`实例。现在，我们使用之前例子上的两个`Function`实例，并执行如下代码：
```
    Function<String,State> lookup = Functions.forMap(stateMap);
    Function<State, String> stateFunction = new StateToCityString();
    Function<String,String> composed =
    Functions.compose(stateFunction ,lookup);
```
调用`composed.apply("NY")`会返回如下结果：
```
    "Albany,Buffalo,NewYorkCity"
```
详细的分析下方法调用的顺序。组合的`Function`获取NY为参数并调用`lookup.apply()`。从`lookup.apply()`方法返回的值又作为`stateFunction.apply()`的参数。最终，`stateFunction.apply()`方法的结果被返回给调用者。诺不使用组合的function,那么上面的例子看起来是这样的：
```
    String cities = stateFunction.apply(lookup.apply("NY"));
```
