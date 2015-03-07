# Getting help with the toString method

>**新版本中`Objects.ToStringHelp`已经是Deprecated的了，使用`MoreObjects.toStringHelper(Object)`替换。**

尽管在debug的时候，`toString`方法十分重要；但把这个方法写好，却很乏味。使用`Objects`类的`toStringHelper`方法会使得这个工作更容易一些。
看看下面的例子类，仔细观察下`toString(`方法：

```
public class Book implements Comparable<Book> {
    private Person author;
    private String title;
    private String publisher;
    private String isbn;
    private double price
....

    public String toString() {
    return Objects.toStringHelper(this)
    .omitNullValues()
    .add("title", title)
    .add("author", author)
    .add("publisher", publisher)
    .add("price",price)
    .add("isbn", isbn).toString();
}
```

`toString` 方法内到底发生了啥？:
- 首先，我们在创建`Objects.ToStringHelp`实例的方法中传进`Book`对象引用。
- 其次，`omitNullValues`方法调用会从以添加的属性中排除任何的空属性。
- 最后，每个调用`add`方法提供一个标签和属性，用于添加到代表Book对象的字符串中去。

一个运行后的例子：
```
Book{title=guava, author=1, publisher=persone, price=1.1, isbn=123123}
```
