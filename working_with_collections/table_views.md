# Table views
table提供了几个方法，可以获取到table底层数据的不同视图。
```
Map<Integer,String> columnMap = table.column(1);
Map<Integer,String> rowMap = table.row(2);
```

`column`方法返回一个map，这个map的key是所有的行值，value则是所有给定列的值。`row`返回的则相反，返回给定行的列-值映射。table返回的map是活的视图，修改columnMap、rowMap和原始的table都会反映到其他的试图上。还有其他的table实现，如下：

1.ArrayTable，底层使用二维数组。

2.ImmutableTable，由于ImmutableTable在建立之后不能被修改。使用ImmutableTable.Builder添加行，key和value。通常用一个fluent结果来更容易的构造出对象。

3.TreeBasedTable，其中row和colum key是有序的，可以使用自然顺序，也可以为row和colum key指定特定的comparators。


