# AsyncEventBus
我们之前就陈述过，要保证事件处理方法尽量轻量，因为EventBus是顺序的处理所有的事件。当然，我们还有另外的可选的AsyncEventBus类。AsyncEventBus类提供的功能EventBus完全相同，但是需要提供java.util.concurrent.Executor实例用于异步地执行处理方法。

#Creating an AsyncEventBus instance
创建AsyncEventBus实例和EventBus实例的方法类似:
```
AsyncEventBus asyncEventBus = new AsyncEventBus(executorService);
```
通过提供一个先创建的ExecutorService实例，就可以构造一个AsyncEventBus实例了。同样，可以可选的提供一个字符串标识，用于标识EventBus。当订阅者接收到的事件可能执行较的处理时，使用AsyncEventBus就会十分有帮助。
