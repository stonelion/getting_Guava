# Using the Sets.union method
`Sets.union`方法使用两个集合，返回两个集合中所有元素的`SetView`实例，看看如下的代码：
```
@Test
public void testUnion(){
    Set<String> s1 = Sets.newHashSet("1","2","3");
    Set<String> s2 = Sets.newHashSet("3","2","4");
        Sets.SetView<String> sv = Sets.union(s1,s2);
        assertThat(sv.size()==4 && sv.contains("2") && sv.contains("3") && sv.contains("4") && sv.contains("1"),is(true));
}
```
