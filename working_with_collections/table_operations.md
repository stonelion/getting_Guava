# Table operations
如下则是一些table的常用例子:
```
    HashBasedTable<Integer,Integer,String> table = HashBasedTable.create();
    table.put(1,1,"Rook");
    table.put(1,2,"Knight");
    table.put(1,3,"Bishop");
    boolean contains11 = table.contains(1,1);
    boolean containColumn2 = table.containsColumn(2);
    boolean containsRow1 = table.containsRow(1);
    boolan containsRook = table.containsValue("Rook");
    table.remove(1,3);
    table.get(3,4);
```

上面例子中的方法，同我在map中看到的并没什么不同。但是，我们以比传统map结构更简洁的方式访问到值。
