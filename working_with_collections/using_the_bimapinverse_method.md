# Using the BiMap.inverse method
现在，让我们看看`inverse`方法的时候：
```
@Test
public void testBiMapInverse() throws Exception {
    BiMap<String,String> biMap = HashBiMap.create();
    biMap.put("1","Tom");
    biMap.put("2","Harry");

    assertThat(biMap.get("1"),is("Tom"));
    assertThat(biMap.get("2"),is("Harry"));
    BiMap<String,String> inverseMap = biMap.inverse();
    assertThat(inverseMap.get("Tom"),is("1"));
    assertThat(inverseMap.get("Harry"),is("2"));
}
```
上面的例子中，我们添加key-value对： `("1","Tom")`
`("2","Harry")`。断言"1"映射到值"Tom","2"映射到值"Harry"。然后，我们在原始的BiMap上调用`inverse`。并断言 "Tom"
映射为"1"，"Harry"映射为"2"。尽管，我们在这里只是表述了
`HashBiMap`的这个方法，`EnumBiMap`,`EnumHashBiMap`,`ImmutableBiMap`，同样也实现了这个方法。
.
