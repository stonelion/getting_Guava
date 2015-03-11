# Guidelines for using the Function interface
尽管匿名类功能有效的作为闭包存在，但是其语法笨重，并且如果过多的使用也会使得你的代码难以维护和阅读。

例如，考虑下典型的命令式方法来取得同样的目标：

```
public String formatDate(Date input) {
    return nw SimpleDateFormat("dd/mm/yyyy").format(input);
}
```
比较下匿名类实现`Function`接口的例子。最后这个例子反而可读性更高。如果你的某个类有个`Date`类型的成员属性, 而且有个方法返回期望字符串格式的`Date`，那么最好以后面这个例子那样实现。

然而，如果持有个`Date`对象的集合，并且需要获得一个含有代表这些日期的字符串list，`Function`接口可能会是更好的方式。

