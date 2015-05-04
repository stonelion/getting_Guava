# Using the FutureCallback
使用FutureCallback接口十分容易，与在ListenableFuture接口上注册回调的方式相类似,当然我们不直接添加FutureCallback到ListenbleFuture。相反，我们使用Futures.addCallback方法。Futures类是静态工具类的集合，用于处理Future实例。让我们看看例子。
先看看一个简单的实现FutureCallback接口：
```
public class FutureCallbackImpl implements FutureCallback<String> {
    private StringBuilder builder = new StringBuilder();
    @Override
    public void onSuccess(String result) {
        builder.append(result).append(" successfully");
    }
    @Override
    public void onFailure(Throwable t) {
        builder.append(t.toString());
    }
    public String getCallbackResult() {
        return builder.toString();
    }
}
```
其中，我们在onSuccess中捕获结果，附加文本"successfully"到结果中。如果发生了错误，我们从Throwable对象上获取错误消息。现在，我们放置所有代码在一起：

```
ListenableFuture<String> futureTask = executorService.submit(new Callable<String>(){
        @Override
        public String call() throws Exception{
            return "Task completed";
        }
    });
FutureCallbackImpl callback = new FutureCallbackImpl();
Futures.addCallback(futureTask, callback);
callback.getCallbackResult();
//假设运行成功，会返回"Task completed successfully"
```
这个例子上，我们够着ListenableFuture接口，实现FutureCallback接口，并注册在ListenableFuture实例完成时运行的代码。实际例子上，我们直接的访问结果。特别地，我们并不想从FutureCallback实例上直接访问结果，而是让FutureCallback异步地的处理其所持有的结果。如果所提供的FutureCallback实例是要执行较为耗时的操作，那么使用下面签名的 Futures.addCallback方法则会更好：
```
Futures.addCallback(futureTask,callback,executorService);
```
使用这个签名的函数，FutureCallback操作会在所提供的ExecutorService线程上执行。否则，初始执行ListenableFuture实例的线程会执行FutureCallback操作。这个行为类似ThreadPoolExecutor.CallerRunsPolicy,
也就是说任务会在调用线程上执行。
