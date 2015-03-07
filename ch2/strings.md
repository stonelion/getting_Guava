# Strings
`Strings`类提供了一些处理字符串十分有用的方法。
你是否写过像下面这样的代码？
```
    StringBuilder builder = new StringBuilder("foo");
    char c = 'x';

    for(int i=0; i<3; i++){
        builder.append(c);
    }
    return builder.toString();
```
上面的例子，我们用了6行的代码，现在我们用一行代码替代它
```
    Strings.padEnd("foo",6,'x');
```
需要注意的是第二个参数，6是指定返回字符串的最小长度，而不是x字符追加到原字符串的次数。如果所提供的字符串长度大于或等于6,那么并不会对字符串进行追加。还有个功能相反但签名相同的`padStart`方法，这个方法插入字符到字符串的前面，直到满足最小长度。

`Strings`类上还有3个处理可能null值字符串十分有用的方法：
- `nullToEmpty`:这个方法使用字符串作为参数，如果这个字符串非null或长度大于0，则返回原字符串，否则返回""。
- `emptyToNull`:这个方法执行的效果与`nullToEmpty`类似，但是，如果字符串参数为null或是一个空字符串，则会返回null值。
- `isNullOrEmpty`:这个方法对字符串null和长度检查，如果字符串是null或空(长度为0)，则会放回true。

对所有作为参数传入的任意字符串对象使用`nullToEmpty`方法，是一个好的习惯。

