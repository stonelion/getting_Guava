# RateLimiter
RateLimiter类操作有点像信号量，但是并非限制并发线程的访问个数，RateLimiter类而是限制访问的时间，就是每秒有多少线程可以访问资源。我建立一个RateLimiter通过如下方式：
```
RateLimiter limiter = RateLimiter.create(4.0);
```
这里，我们调用create方法，并传递double,4.0,指明我们不想每秒提交超过4个任务。我们放置RateLimiter到那些需要限制调用频率的地方。使用的方式如同我们使用信号量那样。如下所示：
```
limiter.acquire();
executor.submit(runnable);
```
这个例子上，我们调用acquire方法，这个方法会阻塞线程，直到线程获得允许并访问资源。如果我们不想使用阻塞，我们可以这么做：

```
    If(limiter.tryAcquire()){
        doSomething();
    }else{
        //Boo can't get in
        doSomethingElse();
    }
```
这里，我们调用tryAcquire,如果资源可用则立即获取，否则，我们执行后面的代码。如果可以获取资源tryAcquire方法返回true，否则返回false。同样还有另一个版本的tryAcquire方法，我们可以指定调用方法的超时时间。
