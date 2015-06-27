# RemovalListener
正如名字所暗示的，RemovalListener，当entry从缓存中被删除，则通知。 RemovalListener则这样的被参数化：
```
RemovalListener<K,V>
```
其中，K是我们想要监听的key类型，V是移除的时我们想要通知的value类型。如果我们想知道任意被删除的entry，我们可以简单的使用Object作为key和value。
