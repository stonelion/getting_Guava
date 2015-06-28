# Sources and Sinks
Guava I/O对读和写文件称为Sources和Sinks。Sources和Sinks
滋生并不是streams', readers', 或writers'对象，而是相似的provider。

Source and Sink可以由两种方式使用：
- 我们可以从provider上抽出底层的stream。provider上返回的stream，完全是一个新的实例，独立于任何其他已经被返回的实例。调用者拿到底层的流对象，并负责关闭这个流。
- 一些基础的工具方法用于执行我们希望的基础操作，例如从stream读，写stream。当通过Sinks或Sources执行读和写，我们需要处理流的打开和关闭。每个操作都会引起新stream的打开和关闭。

目前有两种类型的Sources：`ByteSource`和`CharsSource`。同样，有两种类型的Sinks：`ByteSink` 和 `CharSink`。不同的Source和Sink类提供的功能是相似的，不同点在于我们需要处理的是字符或是元素byte。Files类提供了一些使用ByteSink和CharSink操作文件的方法。我们可以通过Files、ByteStreams或CharStreams类的静态工厂，建立ByteSource, ByteSink, CharSource,或CharSink。

