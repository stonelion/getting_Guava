# Unsubscribing to events
在某些时候，我们希望关闭事件的接收。这可以通过传递消费对象给eventBus.unregister方法来完成。例如，我们要在某时注销订阅，可以在订阅类上写如下的代码：
```
    public void unregister(){
        this.eventBus.unregister(this);
    }
```
当这个方法被调用，指定的实例会停止接收事件。而其他的实例还是会接受事件通知。
