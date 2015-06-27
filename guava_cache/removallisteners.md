# RemovalListeners
RemovalListeners可以让我们容易的用异步处理删除通知事件。
异步的方法如下：
```
RemovalListener<String,TradeAccount> myRemovalListener = new RemovalListener<String, TradeAccount>() {
    @Override
    public void onRemoval(RemovalNotification<String, TradeAccount> notification) {
    //Do something here
    }
};
```
```
RemovalListener<String,TradeAccount> removalListener =
RemovalListeners.asynchronous(myRemovalListener,executorService);
```
其中，我们使用之前构造的RemovalListener和ExecutorService。然后作为参数传递给asynchronous方法。我们得到可以异步处理删除通知的RemovalListener实例。这一步应该要定义在注册RemovalListener对象到CacheBuilder实例之前。
