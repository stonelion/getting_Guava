# FutureFallback
FutureFallback用于在Future实例失败的时候作为副本或默认值。FutureFallback是只有一个方法的接口，create(Throwable t)。通过接受一个Throwable实例，我们可以决定是否我们应该尝试恢复、返回默认值或者传递异常。看看下面的例子：
```
public class FutureFallbackImpl implements FutureFallback<String>{
    @Override
    public ListenableFuture<String> create(Throwable t) throws Exception {
        if (t instanceof FileNotFoundException) {
            SettableFuture<String> settableFuture =
            SettableFuture.create();
            settableFuture.set("Not Found");
            return settableFuture;
        }
        throw new Exception(t);
    }
}
```
这个简单的例子中，假设我们尝试异步的从命令的文件，但是如果没有找到的话，我们并不关心；所以，我们建立一个Future对象，并设置值为“Not Found”。否则，我们只是传递异常。
