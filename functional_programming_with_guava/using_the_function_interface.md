# Using the Function interf
函数式编程强调使用函数来达到目的,而不是改变状态。这与命令式编程截然相反，这种方式依赖状态的改变，而且大部分的开发人员都熟悉这种方式。Guava中的`Function`接口，让我们可以导入一些函数式编程到我们的Java代码。

`Function`接口只包含两个方法：
```
    public interface Function<F,T> {
        T apply(F input);
        boolean equals(Object object);
    }
```
如果对象A等于对象B，那么在对象A上调用`apply`方法的结果和应该和在对象B上调用的结果是一样的。`apply`方法需要一个输入对象，处理后返回一个输出对象。一个良好的`Function`实现应该是没有副作用的，也就是说以参数传递进来的对象，在调用`apply`方法之后，还是应该保持未修改的状态。看看这个例子，接受`java.util.Date`对象，然后返回格式化后的日期字符串。

```
public class DateFormatFunction implements Function<Date,String> {
    @Override
    public String apply(Date input) {
        SimpleDateFormat dateFormat = new SimpleDateFormat("dd/mm/yyyy");
        return dateFormat.format(input);
    }
}
```
尽管这个例子看起来还十分简单，但是证实了`Function`接口的目的，即转换一个对象，同时隐藏实现。例子中我们使用了实现`Function`接口的类，我们可以简单的使用匿名类在一行中来定义`Function`。看看下面的例子：
```
Function<Date,String> function = new Function<Date, String>() {
    @Override
    public String apply(Date input) {
        return new SimpleDateFormat("dd/mm/yyyy").format(input);
    }
};
```
这与上面的例子没什么不同；一个使用实现`Function`接口的类，一个则使用匿名类。使用实现`Function`接口类的一个好处是可以依赖注入来传递`Function`接口到协作类，并增加代码的内聚度。
