# Range
`Range`类让我们可以建立特定的区间，或由端点定义的值区间，最后可以作为`Comparable`类型存在。Range对象可以定义为闭区间或开区间。在复杂的代码里面Range则可以更容易的被理解：
```
Range<Integer> numberRange = Range.closed(1,10);
//两个都返回true，都落在区间内。
numberRange.contains(10);
numberRange.contains(1);
Range<Integer> numberRange = Range.open(1,10);
//两个都返回false，都不落在区间内。
numberRange.contains(10);
numberRange.contains(1);
```
我们可以使用不同的边界条件建立Range对象。例如openClosed, closedOpen, greaterThan, atLeast, lessThan, 和atMost。
这里列举的方法都是返回预期range的静态工厂方法。
