# Cache
Cache接口提供key到value的映射。同样，Cache interface提供的方法远多余基础HashMap所提供的。要放置值到cache中，我们这样可以的调用：
```
put(key,value);
```

Guava 的Cache接口使用传统的put方法，但是从Cache中读取可以有自加载的语法：

```
    V value = cache.get(key, Callable<? Extends V> value);
```

上面的方法，如果值存在会返回值；否则，就会从Callable实例上抽出值，用值关联到特定key，然后在返回值。这个方法可以让我们替代如下的代码模式：

```
    value = cache.get(key);
        if(value == null){
            value = someService.retrieveValue();
            cache.put(key,value);
        }
```
使用Callable对象暗示异步的操作可以能会发生。但是，我们想不异步的执行呢？没有可以使用com.google.common.util.concurrent包里面的Callables类。Callables有一个方法用于处理Callable接口。

```
    Callable<String> value = Callables.returning("Foo");
```

我们再次修改之前的例子：

```
cache.get(key,Callables.returning(someService.retrieveValue());
```

如果没有想要尽可能的取回值，不存在就返回null，我们可以使用getIfPresent(key)，这个方法的行为更像是传统的方式。
还有一些方法用于失效缓存中的值。如下：

- invalidate(key): 这个方法丢弃这个key存储的任何值。
- invalidateAll(): 这个方法丢弃cache中的所有值。
- invalidateAll(Iterable<?> keys): 这个方法丢弃所有的给定key的值。
