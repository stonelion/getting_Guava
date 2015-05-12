# LoadingCache
LoadingCache接口继承自Cache接口,添加了自己加载功能。看看下面的代码：
```
    Book book = loadingCache.get(id);
```
如果book对象在调用get方法的时候不可用，那么LoadingCache会知道如何取回对象，并存储这个对象到cache中，然后放回值。
