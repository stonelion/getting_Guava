# CacheStats
追踪缓存操作会减低性能。要收集缓存统计，我们只需要使用CacheBuilder指定我们想要记录统计：

```
LoadingCache<String,TradeAccount> tradeAccountCache = CacheBuilder.newBuilder().recordStats()
```

激活统计记录，只需要添加recordStats()调用。读取性能统计，我们只需要调用Cache/LoadingCache实例的stats()方法,返回的是CacheStats实例引用。

看看下面的例子：
```
CacheStats cacheStats = cache.stats();
```
CacheStats类上面可以获取到如下的信息：
- 加载新value需要的平均时延
- 请求命中缓存的数值
- 请求不命中缓存的数值
- cache剥夺的数值

还有更多关于缓存性能的信息可供查看。
