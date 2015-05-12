# Refreshing values in the cache
LoadingCache同样提供了一种机制用于刷新缓存中的值:
```
    refresh(key);
```
通过调用refresh，LoadingCache会取回给定key的新value。当前的value并不会被丢弃，直到新value被返回；也就是说，在载入过程中调用get会返回cache中的key。如果在
refresh调用的时候抛出异常，那么原始value会被保存在cache中。需要记住的是，如果value是异步地取回，那么这个方法可能会在实际刷新前返回。
