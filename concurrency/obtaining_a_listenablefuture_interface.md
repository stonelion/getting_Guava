# Obtaining a ListenableFuture interface
正如我们已经知道的，ExecutorService接口在Callable对象提交后返回Future对象。我们要怎样获取到ListenableFuture实例，然后设置我们自己的callback方法呢？我们需要使用ListentingExecutorService包装ExecutorService对象，通过如下方法：

```
ListneningExecutorService service = MoreExecutors.listeningDecorator(executorService);
```

MoreExecutors包含静态方法，用于处理Executor,ExecutorService和ThreadPool实例。
下面的例子，我们把所有的东西都放置到一起：
```
executorService = MoreExecutors.listeningDecorator(Executors.newFixedThreadPool(NUM_THREADS));
ListenableFuture<String> listenableFuture = executorService.submit(new Callable<String>()…);

listenableFuture.addListener(new Runnable() {
    @Override
    public void run() {
        methodToRunOnFutureTaskCompletion();
    }
}, executorService);
```
首先，我们创建固定线程池大小的ExecutorService实例，包装这个实例为ListeningExecutorService。然后，我们提交我们的Callable对象给ListeningExecutorService。最后，我们为任务添加完成时监听器。
ListenableFuture.addListener方法中也有点限制；我们并没有访问到返回的对象，没有为成功或失败的条件指定运行不同的方法。
