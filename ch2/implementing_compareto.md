# Implementing CompareTo
让我们再次使用`Book`类，下面的例子是典型的`compareTo`方法的实现：
```
public int compareTo(Book o) {
    int result = this.title.compareTo(o.getTitle());
    if (result != 0) {
        return result;
    }

    result = this.author.compareTo(o.getAuthor());
    if (result != 0) {
        return result;
    }

    result = this.publisher.compareTo(o.getPublisher());
    if(result !=0 ) {
        return result;
    }

    return this.isbn.compareTo(o.getIsbn());
}
```

现在，让我们使用`ComparisonChain`类来实现`compareTo`:

```
public int compareTo(Book o) {
    return ComparisonChain.start()
    .compare(this.title, o.getTitle())
    .compare(this.author, o.getAuthor())
    .compare(this.publisher, o.getPublisher())
    .compare(this.isbn, o.getIsbn())
    .compare(this.price, o.getPrice())
    .result();
}
```

很显然，第二个例子更紧凑，更容易阅读。`ComparisonChain`类会在首个非0结产生时候停止比较，只有当所有的比较结果都是0的情况下才会返回0。
