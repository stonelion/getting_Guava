# Accounting for null
在排序的时候，我们需要考虑如何处理null值。把null放到最前面，还是最后面？Ordering则会使得这个决定非常简单:
```
Ordering.from(comparator).nullsFirst();
```
同样还有一个类似的方法Ordering.nullsLast，把null值放到集合的最后。
