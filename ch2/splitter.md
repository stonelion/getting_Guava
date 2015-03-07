# Using the Splitter class
另一个我们时常遇到的场景是：用分隔符把字符串切开，然后获得一个字符串各部分的数组。

但是`String.split`方法会遗漏某些我们需要的元素，看看下面例子中出现的问题。

```
String testString = "Monday,Tuesday,,Thursday,Friday,,";
//切出来的部分是[Monday, Tuesday, , Thursday,Friday]
String[] parts = testString.split(",");
```
正如所见，`String.split`方法移除了最后两个组成字符串的实体。
某些场景中，这可能是你想要的行为，但是这应该留给程序员决定，而且不应该默认的发生。

`Splitter`类执行`Joiner`类相反的功能。`Splitter`可以使用单一字符，固定字符串，`java.util.regex.Pattern`包，正则表达式字符串或`CharMatcher`类。

```
    Splitter.on('|').split("foo|bar|baz");
    Splitter splitter = Splitter.on("\\d+");
```

正如上面的例子，一个`Splitter`实例使用'|'字符，另一个`Splitter`实例使用正则表达式，这个表达式会切分一个或多个字符串中连续的数字。

`Splitter`类可以使用`trimResults`方法来处理任何的前导或后继的空白符;

```
    //使用'|'切分，移除任何前导或后继的空白符
    Splitter splitter = Splitter.on('|').trimResults();
```

如同`Joiner`类，`Splitter`创建之后就是不可变的了，所以要注意在创建`Splitter`类之后，再次的调用`trimResults`方法。

例子：
```
    Splitter splitter = Splitter.on('|');
    //下面的调用会返回一个新的实例，不会修改原始的实例。
    splitter.trimResults();
    //结果还是会包含空的元素
    Iterable<String> parts = splitter.split("1|2|3|||");
```

`Splitter`类也有一个和`Joiner`类似相一致的`MapJoiner`就是`MapSplitter`类。
`MapSplitter`类使用这样的字符串进行切分：键和值由一个分隔符隔开，并且键值对由另外一个字符隔开。

```
//MapSplitter是作为Splitter的内部类
Splitter.MapSplitter mapSplitter = Splitter.on("#").
withKeyValueSeparator("=");
```

看看如下的测试用例：
```
@Test
public void testSplitter() {
    String startString = "Washington D.C=Redskins#New York City=Giants#Philadelphia=Eagles#Dallas=Cowboys";

    Map<String,String> testMap = Maps.newLinkedHashMap();
    testMap.put("Washington D.C","Redskins");
    testMap.put("New York City","Giants");
    testMap.put("Philadelphia","Eagles");
    testMap.put("Dallas","Cowboys");
    Splitter.MapSplitter mapSplitter =
    Splitter.on("#").withKeyValueSeparator("=");
    Map<String,String> splitMap = mapSplitter.split(startString);
    assertThat(testMap,is(splitMap));
}
```
