# Concurrency
EventBus并不会多线程的调用处理方法，除非处理方法使用`@AllowConcurrentEvent`注解标记。通过使用`@AllowConcurrentEvent`注解标记一个处理方法，我们就假设我们的处理方法是线程安全的。使用`@AllowConcurrentEvent`注解方法并不会注册到EventBus上。

