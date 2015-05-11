# AsyncFunction
AsyncFunction接口和我们在第3章上介绍的Function接口十分类似。这两个接口接收输入对象。不同的是AsyncFunction接口返回ListenableFuture最为输出对象。

我们调用ListenableFuture.get方法取回AsyncFunction接口处理后的结果当我们想要异步地执行转换逻辑，而不是阻塞的调用(虽然任务还没有完成的时候调用Future.get方法会阻塞)的时候，可以使用AsyncFunction接口。但是AsyncFunction接口并不会异步的执行转换逻辑；而只是返回一个Future实例。
看看下面代码例子：
```
public class AsyncFuntionSample implements AsyncFunction<Long,String> {
    private ConcurrentMap<Long,String> map = Maps.newConcurrentMap();
    private ListeningExecutorService listeningExecutorService;

    @Override
    public ListenableFuture<String> apply(final Long input) throws Exception {
    if(map.containsKey(input)) {
        SettableFuture<String> listenableFuture = SettableFuture.create();
        listenableFuture.set(map.get(input));
        return listenableFuture;
    }else{
        return listeningExecutorService.submit(new Callable<String>(){
        @Override
        public String call() throws Exception {
            String retrieved = service.get(input);
            map.putIfAbsent (input,retrieved);
            return retrieved;
        }
    });
    }
}
```
我们这个类实现AsyncFunction接口，并且包含一个ConcurrentHashMap实例。当我们调用apply方法时，我们会首先查看下map中有没有这个值，输入对象作为key。如果我们在map中找到值，我们使用SettableFuture类构造出Future对象，并且设置为从map中取出的对象。否则，我们返回提交Callable给ExecutorService放回的Future对象。同样也会放置返回的值到map中去。
