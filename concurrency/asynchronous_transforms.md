# Asynchronous Transforms
我们已经在本章中了解了AsyncFunction接口，和它是如何用于异步地转换输入对象。Futures类有一个transform方法，这个方法可以让我很容易的使用AsyncFunction接口：
```
ListenableFuture<Person> lf =Futures.transform(ListenableFuture<String> f,AsyncFunction<String,Person> af);
```
Futures.transform方法返回ListenableFuture实例，这个实例的结果是对传递进函数的ListenableFuture进行求值再执行异步转换得出的。
