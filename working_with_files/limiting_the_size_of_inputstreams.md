# Limiting the size of InputStreams
ByteSteams.limit方法使用InputStream和一个long值作为参数，并返回一个包装了的InputStream，这个InputStream只会读取与给定long值相等的byte数。
```
@Test
public void limitByteStreamTest() throws Exception {
    File binaryFile = new File("src/main/resources/sample.pdf");
    BufferedInputStream inputStream = new BufferedInputStream(new FileInputStream(binaryFile));
    InputStream limitedInputStream = ByteStreams.limit(inputStream,10);
    assertThat(limitedInputStream.available(),is(10));
    assertThat(inputStream.available(),is(218882));
}
```
