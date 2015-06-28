# Copying from a ByteSource class to a ByteSink class
首先，我们使用ByteSource和ByteSink实例这一抽象级别进行处理；并不需要知道他们初始的源是什么。其次，所有资源的开和关闭都由我们处理。
```
@Test
public void copyToByteSinkTest() throws Exception {
    File dest = new File("src/test/resources/sampleCompany.pdf");
    dest.deleteOnExit();
    File source = new File("src/main/resources/sample.pdf");
    ByteSource byteSource = Files.asByteSource(source);
    ByteSink byteSink = Files.asByteSink(dest);
    byteSource.copyTo(byteSink);
    assertThat(Files.toByteArray(dest),
    is(Files.toByteArray(source)));
}
```

