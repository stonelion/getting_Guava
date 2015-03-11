# Using the Functions.forMap method
`forMap`方法使用`Map<K,V>`,返回一个`Function (Function<K,V>)`,这个`Function`的`apply`方法执行map查询。
例如，假设如下的类代表美国中的州：
```
public class State {
    private String name;
    private String code;
    private Set<City> mainCities = new HashSet<City>();
}
```
假设你有一个名字为stateMap的map，类型为`Map<String,State>`，其中key为州的缩写。现在，建立一个查询州代码的`Function`，可以简单的通过如下方法做到：

```
    Function<String,State> lookup = Functions.forMap(stateMap);
    //Would return State object for NewYork
    lookup.apply("NY");
```

使用`Functions.forMap`时还需要另外注意。如果给定的key在map中没有被发现，那么`Function`会抛出一个`IllegalArgumentException`异常。很遗憾，目前没有其他版本的`Functions.forMap`。
