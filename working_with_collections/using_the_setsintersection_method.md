# Using the Sets.intersection method
`Sets.intersection` 方法返回一个不可修改的`SetView`实例，包含在两个集合实例中找到的元素。让我们来看看例子：

```
@Test
public void testIntersection(){
    Set<String> s1 = Sets.newHashSet("1","2","3");
    Set<String> s2 = Sets.newHashSet("3","2","4");
    Sets.SetView<String> sv = Sets.intersection(s1,s2);
    assertThat(sv.size()==2 && sv.contains("2") && sv.contains("3"),is(true));
```
