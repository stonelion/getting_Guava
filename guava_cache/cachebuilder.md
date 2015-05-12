# CacheBuilder
CacheBuilder类通过Builder模式，提供获取Cache和LoadingCache实例的一种途径。有许多选项我可以对cache实例进行指定。第一个例子，如何指定cache entry在载入之后的失效时间：

```
LoadingCache<String,TradeAccount> tradeAccountCache =
    CacheBuilder.newBuilder()
    .expireAfterWrite(5L, TimeUnit.Minutes)
    .maximumSize(5000L)
    .removalListener(new TradeAccountRemovalListener())
    .ticker(Ticker.systemTicker())
    .build(new CacheLoader<String, TradeAccount>() {
        @Override
            public TradeAccount load(String key) throws Exception {
                return tradeAccountService.getTradeAccountById(key);
            }
    });
```

```
public class TradeAccount {
    private String id;
    private String owner;
    private double balance;
}
```

1. 首先，我们调用expireAfterWrite，这个会自动的从cache中删除满足给定时间的entry，例子上是5分钟。
2. 其次，我们使用maximumSize指定cache最大的值为5000。在chache到达最大值的时候，使用LRU算法删除entry。
3. 再次,我们添加RemovalListener实例，会在entry被删除的时候收到通知。
4. 然后，我们添加Ticker实例，通过调用ticker方法，为entry死亡，提供纳秒级别的精确程度。
5. 最后，我们调用build方法，并传递一个新的CacheLoader实例，这个实例用于在给定key的value不存在的时候，取回TradeAccount对象。

```
LoadingCache<String,Book> bookCache = CacheBuilder.newBuilder()
    .expireAfterAccess(20L,TimeUnit.MINUTES)
    .softValues()
    .removalListener(new BookRemovalListener())
    .build(new CacheLoader<String, Book>() {
        @Override
        public Book load(String key) throws Exception
        {
            return bookService.getBookByIsbn(key);
        }
    });
```
这个例子上，我们的做法就有点不同。
1. 指定我们想要entry 在最后访问20分钟之后死亡。使用expireAfterAccess方法。
2. 没有明确限制cache的大小为指定值，我们让JVM限制其大小。通过调用softValues()，我们让value包装为SoftReferences。SoftReferences是可以被垃圾收集的，并且使用JVM维度的LRU算法。
3. 最后, 我们添加RemovalListener和CacheLoader。


```
LoadingCache<String,TradeAccount> tradeAccountCache =
    CacheBuilder.newBuilder()
        .concurrencyLevel(10)
        .refreshAfterWrite(5L,TimeUnit.SECONDS)
        .ticker(Ticker.systemTicker())
        .build(new CacheLoader<String,TradeAccount>() {
            @Override
            public TradeAccount load(String key) throws Exception {
                return tradeAccountService.getTradeAccountById(key);
            }
        });
```
1. 提供并发更新操作的指标量，使用值10调用concurrencyLevel方法。如果没有明确的设置，那么默认的值是4.
2. 并非明确的删除值，而是在超过时间之后刷新value。注意下，触发刷新value是接到请求和时间限制。
3. 我们添加Ticker实例，通过调用ticker方法，为entry死亡，提供纳秒级别的精确程度。
4. 最后，指定loader，调用build方法。
