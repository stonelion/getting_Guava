# BaseEncoding
当处理二进制数据，有时候就需要转换Byte代表的数据到ASCII字符。当然，也需要从编码后的byte转换成元素的形式。
```
@Test
public void encodeDecodeTest() throws Exception {
    File file = new File("src/main/resources/sample.pdf");
    byte[] bytes = Files.toByteArray(file);
    BaseEncoding baseEncoding = BaseEncoding.base64();
    String encoded = baseEncoding.encode(bytes);
    assertThat(Pattern.matches("[A-Za-z0-9+/=]+",encoded),is(true));
    assertThat(baseEncoding.decode(encoded),is(bytes));
}
```
我们使用一个二进制文件，编码byte到base64字符串。并断言字符串全部是由ASCII字符组成。

```
    @Test
    public void encodeByteSinkTest() throws Exception{
        File file = new File("src/main/resources/sample.pdf");
        File encodedFile = new File("src/main/resources/encoded.txt");
        encodedFile.deleteOnExit();
        CharSink charSink = Files.asCharSink(encodedFile,Charsets.UTF_8);
        BaseEncoding baseEncoding = BaseEncoding.base64();
        ByteSink byteSink = baseEncoding.encodingSink(charSink);
        ByteSource byteSource = Files.asByteSource(file);
        byteSource.copyTo(byteSink);
        String encodedBytes = baseEncoding.encode(byteSource.read());
        assertThat(encodedBytes,is(Files.toString(encodedFile,Charsets.UTF_8)));
    }
```
