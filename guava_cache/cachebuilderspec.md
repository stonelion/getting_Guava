# CacheBuilderSpec
CacheBuilderSpec可以通过使用传递代表CacheBuilder设置的字符串来建立CacheBuilder实例(如果使用了这一种方式，我们就不能够在编译时检查错误的string，这样的string会导致运行时错误)。
下面的例子是可用的字符串建立CacheBuilderSpec实例：

```
String configString = "concurrencyLevel=10,refreshAfterWrite=5s"
```
对于指定time (refreshAfterWrite,expireAfterAccess, 等等)的属性，整数后面跟随的是间隔的单位，'s', 'm', 'h', 或 'd'。代表秒，分钟，小时，或天数。没有为毫秒和纳秒的选项。我们指定好string之后就可以实例化CacheBuilderSpec类了：

```
CacheBuilderSpec spec = CacheBuilderSpec.parse(configString);
```
之后就就可以使用CacheBuilderSpec类来建立CacheBuilder实例：
```
    CacheBuilder.from(spec);
```
要为builder上添加RemovalListener或者构造LoadingCache，我们可以使用返回的CacheBuilder实例然后调用合适的方法：

```
String spec = "concurrencyLevel=10,expireAfterAccess=5m,softValues";
CacheBuilderSpec cacheBuilderSpec = CacheBuilderSpec.parse(spec);
CacheBuilder cacheBuilder = CacheBuilder.from(cacheBuilderSpec);
cacheBuilder.ticker(Ticker.systemTicker()).removalListener(new TradeAccountRemovalListener()).build(new CacheLoader<String, TradeAccount>() {
    @Override
    public TradeAccount load(String key) throws Exception {
        return tradeAccountService.getTradeAccountById(key);
    }
    });
```
