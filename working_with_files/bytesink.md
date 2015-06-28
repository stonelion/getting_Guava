# ByteSink
ByteSink类表示一个可写byte的资源。我们可以写byte到文件或者是一个目的地，可能为byte数组。要从文件上建立ByteSink，可以这么做：
```
@Test
public void testCreateFileByteSink() throws Exception {
    File dest = new File("src/test/resources/byteSink.pdf");
    dest.deleteOnExit();
    byteSink = Files.asByteSink(dest);
    File file = new File("src/main/resources/sample.pdf");
    byteSink.write(Files.toByteArray(file));
    assertThat(Files.toByteArray(dest),is(Files.toByteArray(file)));
}
```
