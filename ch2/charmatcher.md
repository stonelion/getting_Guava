# CharMatcher
`CharMatcher`类提供了判定特定字符或字符范围是否出现一些功能函数。`CharMatcher`类中的方法让格式化和文本处理更容易。

例如，你有一个多行的字符串，你需要把这个字符格式化成单行用空格隔开：

```
CharMatcher.BREAKING_WHITESPACE.replaceFrom(stringWithLinebreaks,' ');
```
当然也可以使用`replaceFrom`的`CharSequence`版本作为替换值，不用单个字符。

要移除多个tab和空格(也就是连续的),并把这些空白符压缩成一个空格，可以使用如下的代码：

```
@Test
public void testRemoveWhiteSpace(){
    String tabsAndSpaces = "String      with       spaces and
tabs";
    String expected = "String with spaces and tabs";
    String scrubbed = CharMatcher.WHITESPACE.collapseFrom(tabsAndSpaces,' ');
    assertThat(scrubbed,is(expected));
}
```
上面这个测试用例中，我使用一个有多个空格和tab，并替换这些成一个空格，所有这些都在一行代码内完成。

但是，如果我们希望移除掉字符串开头的空格又要如何做？返回的有空格在最前面，可以使用`trimAndCollapseFrom`方法很容易的处理：
```
@Test
public void testTrimRemoveWhiteSpace(){
    String tabsAndSpaces = " String with spaces and tabs";
    String expected = "String with spaces and tabs";
    String scrubbed = CharMatcher.WHITESPACE.trimAndCollapseFrom(tabsAndSpaces,' ');
    assertThat(scrubbed,is(expected));
}
```
尽管列出所有`CharMatcher`类可用的方法有点不切实际，下面的例子并不是替换匹配组的内容，而是保存匹配的字符：
```
@Test
public void testRetainFrom(){
    String lettersAndNumbers = ""foo989yxbar234"";
    String expected = ""989234"";
    String retained = CharMatcher.JAVA_DIGIT.retainFrom(lettersAndNumbers);
    assertThat(expected,is(retained));
}
```
在我们继续之前，需要了解一下`CharMatcher`类最有力的特性: 组合`CharMatcher`类，来创建新的`CharMatcher`类。

例如，我们假设需要建立一个匹配数字或空白符的matcher:
```
    CharMatcher cm = CharMatcher.JAVA_DIGIT.or(CharMatcher.WHITESPACE);
```
这将会匹配任意的数字(Java中所定义的)或空白字符。
处理Java中的String时，`CharMatcher`类十分有用并且具有强大的能力。
