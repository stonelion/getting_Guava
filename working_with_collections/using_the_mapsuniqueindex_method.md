# Using the Maps.uniqueIndex method
`Maps.uniqueIndex`方法需要给定类型的`iterator`或`iterable`和`Function`作为参数。由`iterator/iterable`提供的元素会称为map的value，同时在每个元素上应用`Function`产生这个元素的key。所以，如果我们想重构之前的例子，可以使用如下的形式：
```
List<Book> books = someService.getBooks();
    Map<String,Book>bookMap = Maps.uniqueIndex(books.iterator(),new
    Function<Book, String>(){
     @Override
        public String apply( Book input) {
            return input.getIsbn();
        }
};)
```
这个例子中，我们提供由book列表上获得的`iterator`，定义一个从每本书上抽取ISBN的`function`。ISBN会作为map中Book对象的key。尽管例子使用匿名类建立`Function`，但是如果传递进来的是通过方法调用或依赖注入的话，那么我们可以很容易的修改为`Book`对象生成key的算法，这样不会影响原有代码。
