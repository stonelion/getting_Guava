# Checking for null values

>**新版本中`Objects.firstNonNull`已经是Deprecated的了，使用`MoreObjects.firstNonNull(T first,T second)`替换。**

`firstNonNull`方法使用两个参数并且返回非空的那个参数。

```
String value = Objects.firstNonNull(someString,"default value");
```
`firstNonNull` 方法可以在当你并不确定对象是否是空的情况下，用于作为一种提供默认值的方式。
需要注意的是，如果两个参数都为空，那么会抛出`NullPointerException`错误。
