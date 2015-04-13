# Using the BiMap.forcePut method
为了可以添加相同的value给不同的key，我们需要调用`forcePut(key,value)`。`BiMap.forcePut`调用则会在插入key-value对到map中之前，安静的删除相同value的map entry。很显然，如果插入的是相同的key和value，那么map并不会有什么改变。然而，如果value相同，key不同，则之前的那个key就会被丢弃。下面是一个简单的单元测试表述这一点：
```
@Test
public void testBiMapForcePut() throws Exception {
    BiMap<String,String> biMap = HashBiMap.create();
    biMap.put("1","Tom");
    biMap.forcePut("2","Tom");
    assertThat(biMap.containsKey("1"),is(false));
    assertThat(biMap.containsKey("2"),is(true));
}
```
上面的例子中，我们首先用key = 1添加value = Tom。然后，我们再次用key = 2 添加 value = Tom，这时候我们则是使用`forcePut`方法。最初的key (1)被丢弃，则有key (2)指向 value (Tom)。这个行为看起来完全正确。因为，当倒置方法被调用，是从value映射到key，之前的value应该被覆盖。所以，使用`forcePut`方法明确表述我们需要替换当前的key，而不是得到一个异常的行为。
