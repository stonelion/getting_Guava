# RemovalNotification

RemovalNotification实例是在entry被删除之后RemovalListener上接收到的对象。RemovalNotification实现Map.Entry 接口，我们可以访问到cache上entry实际的key和value。如果entry由于垃圾收集被删除，那么这些value可能会是null。
我们同样可以获取到被删除的原因，通过调用RemovalNotification实例上的getCause()方法，这个方法返回一个RemovalCause
enum。
RemovalCause enum可能的值如下：
- COLLECTED:指示key或value可能被垃圾收集了。
- EXPIRED: 指示entry的最后写或最后读时间超过了限制。
- EXPLICIT: 指示用户手动的删除entry。
— REPLACED: 指示entry实际上没被删，但是值被替换了。
- SIZE: 指示entry被删除，归因与接近Cache大小或到达指定的大小限制。
