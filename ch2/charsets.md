# Charsets
Java内部，有6种各个Java平台都支持的标准字符集。但这并是什么重要的地方，因为并不是经常执行像如下的代码：

```
    byte[] bytes = someString.getBytes();
```
可是使用上述的代码会引起一些问题。不指定你想要获得的byte数组的字符集，而且如果运行系统的默认字符集和你所想要的字符集不同，那么就会出现问题。大家普遍认为使用如下的方法来获得bytes是最好的方式。

```
    try{
        bytes = "foobarbaz".getBytes("UTF-8");
    }catch (UnsupportedEncodingException e){
        //并不会有异常出现，因为UTF-8是必须被支持的。
    }
```
但是这个例子还是有两个问题。
- Java平台上必须支持UTF-8，所以，实际上`UnsupportedEncodingException`错误永远不会被抛出。
- 由于我们使用字符串来指定字符集的定义，我们可能会拼写错误；当然，这会导致异常的抛出。

这些就是`Charsets`类要帮助你做的事情了。`Charsets`类提供
提供了Java平台上被支持的六种字符集的static final引用。
使用`Charsets`类的例子：
```
    byte[] bytes2 = "foobarbaz".getBytes(Charsets.UTF_8);
```
在Java 7中这么做并不值得，因为`StandardCharsets`类同样提供了静态应用。
