# Different Monitor access methods
虽然Monitor提供了几个进入monitor的方法，同样库也提供了5个基础的类型。
1. `Monitor.enter`: Monitor.enter方法会尝试进入monitor，并且会不确定地的阻塞住，直到线程进入monitor。

2. `Monitor.enterIf`: Monitor.enterIf方法需要Monitor.Guard作为参数，并且阻塞进入monitor。一旦这个方法进入monitor，并不会等待条件满足，而是返回boolean指示Monitor 临界区是否进入。

3. `Monitor.enterWhen`: `Monitor.enterWhen`方法同样需要Monitor.Guard作为参数，阻塞等待进入monitor。可是，一旦获得到锁，这个方法会不确定地等待条件被满足。
4. `Monitor.tryEnter`: `Monitor.tryEnter` 方法会尝试访问monitor，但是如果已经被其他线程占用的话，这个方法不会等待获取锁，而是返回boolean值，指示Monitor临界区是否可以进入。
5. Monitor.tryEnterIf: 这个方法仅当锁可用，条件被满足时，立即进入monitor。否则，这个方法不会等待锁，或条件被满足，而是返回boolean指示Monitor临界区是否进入。

所有这些方法，都有一个变体，这个变体使用参数(long 和 TimeUnit)，用于指定获取锁、等待条件被满足锁需要的时间。
