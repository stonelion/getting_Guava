# Loading values
由于LoadingCache的实现期望是线程安全的，对相同key调用get时，cache的加载会阻塞。一旦value被加载成功，那么调用会返回被加载的value给get方法。
然而，对不同key调用get会并发的加载。如果我们还有个key集合，并且要取回每个key的value，可以这样调用：

```
ImmutableMap<key,value> map = cache.getAll(Iterable<? Extends key>);
```

返回给定key在cache中的ImmutableMap。这个map中可能包含缓存的value，新取回的值，或是混合缓存和新取回的值。
