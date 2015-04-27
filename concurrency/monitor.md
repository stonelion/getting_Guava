# Monitor
Guava的Monitor类给我们提供的有多重condition和移除通知所有线程的可能性，使用明确通知机制而不是非明确机制。
看看下面的例子：
```
public class MonitorSample {
    private List<String> list = new ArrayList<String>();
    private static final int MAX_SIZE = 10;
    private Monitor monitor = new Monitor();
    private Monitor.Guard listBelowCapacity = newMonitor.Guard(monitor) {
        @Override
        public boolean isSatisfied() {
            return list.size() < MAX_SIZE;
        }
    };

        public void addToList(String item) throws InterruptedException{
            monitor.enterWhen(listBelowCapacity);

            try {
                list.add(item);
            } finally {
                monitor.leave();
            }
    }
}
```
先看例子中有趣的部分。首先，我们建立一个Monitor类的实例。之后我们使用新建立的Monitor实例，来构造Guard类实例，这个类上面有个叫isSatisfied的抽象方法。如果我们的list容器小于10，则会返回true。最后，在addToList方法内，线程会进入到Monitor，并且会在我们Guard条件计算为true的情况下添加元素到list中。否则，线程则会等待。注意下，更高的可读性enterWhen方法，这个方法允许线程在满足Guard条件的情况下进入临界区。同样也要注意到，我们没有明确的唤醒任何线程；完全是隐式地唤醒满足Guard条件的线程。
