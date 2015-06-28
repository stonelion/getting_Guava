# ByteSource
ByteSource类代表了一个可读的byte源。一般而言，我们希望底层的byte源是文件，但是也有可能是一个byte数组。我们可以通过使用Files类上的静态方法从文件对象上建立ByteSource：
```
@Test
public void createByteSourceFromFileTest() throws Exception {
    File f1 = new File("src/main/resources/sample.pdf");
    byteSource = Files.asByteSource(f1);
    byte[] readBytes = byteSource.read();
    assertThat(readBytes,is(Files.toByteArray(f1)));
}
```
