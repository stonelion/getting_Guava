ListenableFuture# Concurrency
- Monitor类功能上作为互斥锁(Mutex),确保线性的访问代码中定义的区域，与synchronized关键字十分类似，但是提供了更简单的语句和一些有用的额外特性。
- ListenableFuture类,与java中Listenable类的功能类似，我们可以注册一个callback方法，一旦Future字自身执行完毕则会执行这个方法。
- FutureCallback类让我们可以访问到Future task的结果，并可以处理成功或失败的场景。
- SettableFuture, AsyncFunction和FutureFallback类则是一些有用的工具类，处理Future实例和异步转换对象的时候可以使用到。
- Futures类则有一个有用的静态方法来处理Future实例。
- RateLimiter类则限制有多少线程可以访问到资源。这个类与信号量(semaphore)非常像，并非限制访问线程的总数，RateLimiter类的限制则是基于时间。
