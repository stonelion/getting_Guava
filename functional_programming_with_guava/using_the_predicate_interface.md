# Using the Predicate interfac
`Predicate`接口是`Function`接口的表弟。和`Function`接口类似，`Predicate`接口也有两个方法。

看看接口定义：
```
public interface Predicate<T> {
    boolean apply(T input)
    boolean equals(Object object)
}
```
正如之前使用`Function`接口的例子，我们没有更细节的介绍`equals`方法。`apply`方法返回对输入应用`Predicate`的结果。`Function`接口用于转换对象，`Predicate`则是用于过滤对象。这个用于`Predicates`的指导方针同样也适用于`Functions`；不要在更简单的过程方法可以满足的情况下在使用`Predicates`。同样，`Predicate`函数不应该有任何的副作用。
