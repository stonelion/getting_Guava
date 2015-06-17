# Subscribing to events
要让一个对象从EventBus接收到通知，需要如下的三个步骤：
1. 对象需要定义一个只接受一个参数的方法。这个参数应该是对象所希望接收到事件类型。
2. 暴露给时间通知的方法需要用@Subscribe注解。
3. 最后，使用EventBus实例注册对象，传递对象给EventBus.register方法。
