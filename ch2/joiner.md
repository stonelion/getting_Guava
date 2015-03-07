# Using the Joiner class

使用某些分隔符把任意的字符串连接起来，我们通常都会碰到这样的情况。
一般都是从array，list，或者iterable中循环获得到内容，然后把每个元素append给StringBuilder类，再append那个分隔符。
这看起来是个笨重的活，通常会像如下的形式：
```
public String buildString(List<String> stringList, String delimiter){
    StringBuilder builder = new StringBuilder();
        for (String s : stringList) {
            if(s !=null){
                builder.append(s).append(delimiter);
            }
        }
        builder.setLength(builder.length() – delimiter.length());
    return builder.toString();
}
```
当然，需要移除掉附加到最后字符串后面的那个标识符。

这并不是的复杂，但这确实有些公式化的代码，我们可以使用`Joiner`类轻松的解决。

假定，我们使用"|"作为分隔符，但是确实使用`Joiner`类：

```
Joiner.on("|").skipNulls().join(stringList);
```

咋样？是不是更为精简而且也不会因格式化字符串而可能产生错误。

如果你想为null值设置一个替换值，可以这么做：

```
    Joiner.on("|").useForNull("no value").join(stringList);
```

想要愉快的使用`Joiner`类，我们还需要理解一些它的特点。

`Joiner`类并只局限于在字符串上使用。可以丢进去array,iterable或者任意对象的可变参数。结果则是通过调用每个传进来对象的`Object.toString()`方法。

当然，如果没有使用skipNulls或useForNull方法，就会抛出`NullPointerException`错误。

当构建成功，`Joiner`类则是不可变的，因此也是线程安全的，可作为 static final变量。

`Joiner`并非只可以返回字符串，还可以使用`StringBuilder`类:

```
    StringBuilder stringBuilder = new StringBuilder();
    Joiner joiner = Joiner.on("|").skipNulls();
    //返回StringBuilder实例的值为：foo|bar|baz
    joiner.appendTo(stringBuilder,"foo","bar","baz")
```

`Joiner`类可以在实现了Appendable接口的类上使用。

```
    FileWriter fileWriter = new FileWriter(new File("path")):
    List<Date> dateList = getDates();
    Joiner joiner = Joiner.on("#").useForNulls(" ");
    //返回附加了值的FileWriter实例
    joiner.appendTo(fileWriter,dateList);
```

在我继续之前，还有一个特别的方法需要介绍一下;就是,`MapJoiner`方法;`MapJoiner`方法和`Joiner`做相同的事情，但是它用分隔符隔开给定字符串的键-值对。

`MapJoiner`方法如下建立：

```
mapJoiner = Joiner.on("#").withKeyValueSeparator("=");
```

- 调用Joiner.on("#")建立一个Joiner对象。
- `withKeyValueSeparator`方法，使用调用的`Joiner`实例构造出`MapJoiner`对象并返回。

这个单元测试表述了如何使`MapJoiner`

```
@Test
public void testMapJoiner() {
    //Using LinkedHashMap so that the original order is preserved
    String expectedString = "Washington D.C=Redskins#New York City=Giants#Philadelphia=Eagles#Dallas=Cowboys";
    Map<String,String> testMap = Maps.newLinkedHashMap();
    testMap.put("Washington D.C","Redskins");
    testMap.put("New York City","Giants");
    testMap.put("Philadelphia","Eagles");
    testMap.put("Dallas","Cowboys");
    String returnedString = Joiner.on("#").
    withKeyValueSeparator("=").join(testMap);
    assertThat(returnedString,is(expectedString));
}
```
