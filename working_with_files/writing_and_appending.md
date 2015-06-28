# Writing and appending
写并追加一个文件的例子如下：
```
@Test
public void appendingWritingToFileTest() throws IOException {
    File file = new File("src/test/resources/quote.txt");
    file.deleteOnExit();
    String hamletQuoteStart = "To be, or not to be";
    Files.write(hamletQuoteStart,file, Charsets.UTF_8);
    assertThat(Files.toString(file,Charsets.UTF_8),is(hamletQuoteStart));
    String hamletQuoteEnd = ",that is the question";
    Files.append(hamletQuoteEnd,file,Charsets.UTF_8);
    assertThat(Files.toString(file, Charsets.UTF_8),is(hamletQuoteStart + hamletQuoteEnd));
    String overwrite = "Overwriting the file";
    Files.write(overwrite, file, Charsets.UTF_8);
    assertThat(Files.toString(file, Charsets.UTF_8),is(overwrite));
}
```

1. 建立文件用于测试，并保证文件在JVM运行时被删除。
2. 使用Files.write方法写一个String到文件上，并确保写成功3. 然后使用File.append方法追加另一个string并期望结果为文件组合我们添加的string。
4. 最后，我们使用Files.write方法覆盖文件，并确实我们确实覆盖了文件。注意，我们写这个文件5次，并没有打开或者关闭任何的资源。这样，我们的代码可以容易读，减少错误倾向。
