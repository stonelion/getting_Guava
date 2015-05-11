# Applying FutureFallbacks
我们同样了解了FutureFallback接口和接口如何提供我们处理ListenableFuture上的错误。Futures.withFallback方法提供无缝的方式来应用FutureFallback。如下所示：
```
ListenableFuture<String> lf = Futures.withFallback(ListenableFuture<String> f,FutureFallback<String> fb);
```
这个例子上，被返回的ListenableFuture实例，如果执行成功会返回给定的ListenableFuture结果，若不成功则会是FutureFallback实现的结果。
上面的这两个例子，都有一个重载的方法，使用ExceutorService来执行AsyncFunction或FutureFallback的动作。
Futures类上还有一些其他的方法用于处理Future实例。
