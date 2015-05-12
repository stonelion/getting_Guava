# Guava Cache
软件开发中，缓存是一个十分重要的主题。如果至是一个简单的程序，大部分人并不会使用缓存的方式。而是直接使用map。Guava提供的缓存比我们使用HashMap更灵活。但是与EHCache或Memcached相比还是不够健壮。

本章中，我们介绍Guava中提供的缓存功能。我们要详细的表述如下的主题：
- MapMaker类用于创建ConcurrentMap实例
- CacheBuilder类使用fluent构建API，建立LoadingCache和Cache实例
- CacheBuilderSpec类使用格式化的字符串建立CacheBuilder实例
- CacheLoader由LoadingCache实例所使用，用于为给定key获取值。
- CacheStats类提供cache的性能统计。
- 当entry从cache中被删除的时候，RemovalListener会收到通知。
