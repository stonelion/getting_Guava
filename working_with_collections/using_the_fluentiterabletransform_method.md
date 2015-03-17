# Using the FluentIterable.transform method
`FluentIterable.transform`方法是一种映射操作，其中每个元素都应用`Function`。这个操作的输出一个新的与原始长度相同的由转换后对象组成的`iterable`，这可能会转移任意或所有的原始元素。下面就举例`transform`方法，再次使用上面例子中的数据。
```
@Test
public void testTransform() throws Exception {
    List<String> transformedPersonList =
    FluentIterable.from(personList).transform(new Function<Person,String>() {
        @Override
        public String apply(Person input) {
            return Joiner.on('#').join(input.getLastName(),input.getFirstName(), input.getAge());

        }).toList();

        assertThat(transformed.get(1), is("Flintstone#Fred#32"));
}
```
这个例子中，我们转换每一个`personList`中的元素为以`#`隔开的last name,first name和`Person`对象组成的字符串。
首先使用`FluentIterable.from`方法，然后传递`Function`给`transform`用于串联。当最后，我们同样串联了第三个方法，`toList`,返回最后的结果为`List<String>`。同样还有`toSet` , `toMap` , `toSortedList`和`toSortedSet`方法可以用。`toMap`方法以`FluentIterable`中的元素为key，需要`Function`来提value。
`toSortedList`和`toSortedSet`使用一个`Comparator`来指定顺序。
