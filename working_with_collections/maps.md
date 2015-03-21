# Maps
`Maps`是我们日常编程中主要使用的一种数据结构。由于Map的普遍使用，任何让创建和使用更容易的方法会极大提升java程序员的生产力。Guava中的`Maps`工具类显然提供了这种便利。首先，我们查看从以存在的集合对象中构造map的更简单方法。使用一个集合对象，并需要建立一个这些对象的map，这种情况经常发生用于满足某些缓存或使用快速查找。第二个例子，假设我们有一个`Book list`对象，并希望以ISBN号码为key存储这些对象到map中。当然，可行的转换`ist`到`Map`的代码如下：
```
List<Book> books = someService.getBooks();
Map<String,Book> bookMap = new HashMap<String,Book>()
    for(Book book : books){
        bookMap.put(book.getIsbn(),book);
    }
```
尽管代码和直观，但是我们可以做的更好。
