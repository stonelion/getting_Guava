# DeadEvents
当EventBus通过post方法收到事件通知，但当没有注册的订阅者的时候，事件会被包裹到DeadEvent类实例内。有某个类订阅DeadEvent实例，在确保所有事件都有注册消费者的时候是十分有用的。DeadEvent类暴露了getEvent方法，可以用于查看初始未被投递的事件。例如，我们可以提供一个非常简单的类，如下：
```
    public class DeadEventSubscriber {
        private static final Logger logger = Logger.getLogger(DeadEventSubscriber.class);
        public DeadEventSubscriber(EventBus eventBus) {
            eventBus.register(this);
        }

        @Subscribe
        public void handleUnsubscribedEvent(DeadEvent deadEvent){
            logger.warn("No subscribers for "+deadEvent.getEvent());
        }
}
```
这里，我们只是简单的记录下没有被消费的事件。
