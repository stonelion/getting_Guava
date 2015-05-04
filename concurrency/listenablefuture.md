# ListenableFuture
Future对象代表了异步操作的结果。例如：
```
ExecutorService executor = Executors.newCachedThreadPool();
Future<Integer> future = executor.submit(new Callable<Integer>(){
    public Integer call() throws Exception{
        return service.getCount();
    }
});
//取回计算的结果
Integer count = future.get();
```
这个例子上，我们提交一个Callable对象给ExecutorService实例。ExecutorService 实例则会立即返回Future对象;可是，并没说明任务已经完成了。要获取到任务结果，我们调用future.get()方法，如果任务没有完成，调用这个方法会阻塞住。ListenableFuture接口扩展自Future接口，使得我们可以注册回调句柄，在任务执行完毕的时候自动的执行回调。通过调用ListenableFuture.addListener方法完成这个功能，这个方法使用Runnable实例和ExecutorService对象，ExecutorService可以是初始任务提交的相同Executor实例，或者完全是另外一个ExecutorService实例。
