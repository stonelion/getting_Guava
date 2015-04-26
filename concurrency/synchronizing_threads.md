# Synchronizing threads
Java提供了synchronized关键字来完成线性访问的目的。但是使用synchronized也有一些问题。首先，如果我们需要在线程调用wait()，则我们必须使用这样的循环：

```
    while(someCondition){
        try {
            wait();
        } catch (InterruptedException e) {
            //In this case we don't care, but we may want
            //to propagate with Thread.interrupt()
        }
    }
```
其次，如果我们有超过一个可能引起线程进入等待状态的条件的话，则我们必须调用notifyAll()方法，因为我们无法为特定的条件通知线程。使用notifyAll()而不是一定的使用notify()，因为notifyAll唤醒所有的线程竞争获取锁，之后只有一个线程能够执行。Java 5 导入ReentrantLock类，可以用于建立condition。使用ReentrantLock我们可以获得更细粒度的控制，调用newCondition()方法。
现在可以通过调用Condition.signal()(类似notify())方法，唤醒一个在特定条件下等待的线程，也有Condition.signalAll()方法他的作用和调用notifyAll()是一样的。
但是，我们任然还有一些非直接的while循环要编写：
while(list.isEmpty()){
    Condition.await();
}
幸运的是，Guava解决了这个问题，Monitor类。
