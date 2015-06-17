# Creating an EventBus instance
建立一个EventBus实例可以仅通过调用EventBus的构造器来实现:
```
    EventBus eventBus = new EventBus();
```
我们还可以提供可选的字符串参数为EventBus建立标识符。
```
    EventBus eventBus = new EventBus(TradeAccountEvent.class.getName());
```
