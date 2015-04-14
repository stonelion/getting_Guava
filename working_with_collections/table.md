# Table
Map当然是我们日常编程中十分好用的集合。然而有时一个map并不足够；我们需要map的map。虽然有时这十分有用，但是在Java里面建立和使用这个类型却显得有点麻烦。幸运的是，Guava给我们提供了table集合。一个table是有两个key的集合，一个为行(row),一个为列(column)，最后这些key映射到单一的value上。虽然没有比调用map的map特别之处，但是table给我们想要的函数，更容易使用。有几种table的实现，下面的例子，我们会使用
`HashBasedTable`, 存储数据到`Map<R, Map<C, V>>`里面。建立一个`HashBasedTable`则十分容易，看看如下的代码:
```
HashBasedTable<Integer,Integer,String> table = HashBasedTable.create();
//创建初始化5行5列的表
HashBasedTable<Integer,Integer,String> table = HashBasedTable.create(5,5);
//从以存在的table建立table
HashBasedTable<Integer,Integer,String> table = HashBasedTable.create(anotherTable);
```
