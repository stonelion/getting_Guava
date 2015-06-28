# Working with files as strings
有时候我们需要操作或处理文件作为string。
```
@Test
public void readFileIntoListOfStringsTest() throws Exception{
    File file = new File("src/main/resources/lines.txt");
    List<String> expectedLines = Lists.newArrayList("The quick brown","fox jumps over","the lazy dog");
    List<String> readLines = Files.readLines(file,Charsets.UTF_8);
    assertThat(expectedLines,is(readLines));
}
```
每一行都传递进LineProcessor.processLine方法内，该方法发挥一个boolean。文件中的行会继续流式的传递进LineProcessor实例，直到文件结束或LineProcessor.processLine返回false。
假设我们有一个CSV文件，包含如下信息：
```
"Savage, Tom",Being A Great Cook,Acme Publishers,ISBN-123456,29.99,1
"Smith, Jeff",Art is Fun,Acme Publishers,ISBN-456789,19.99,2
"Vandeley, Art",Be an Architect,Acme Publishers,ISBN-234567,49.99,3
"Jones, Fred",History of Football,Acme Publishers,ISBN-345678,24.99,4
"Timpton, Patty",Gardening My Way,Acme Publishers,ISBN-4567891,34.99,5
```
我们想要抽取出每行中书的标题。要完成这个任务，可以写如下的LineProcessor接口实现。

```
public class ToListLineProcessor implements
    LineProcessor<List<String>>{
        private static final Splitter splitter = Splitter.on(",");
        private List<String> bookTitles = Lists.newArrayList();
        private static final int TITLE_INDEX = 1;
        @Override
        public List<String> getResult() {
            return bookTitles;
        }
        @Override
        public boolean processLine(String line) throws IOException {
            bookTitles.add(Iterables.get(splitter.split(line),TITLE_INDEX));
        return true;
}
```

```
@Test
public void readLinesWithProcessor() throws Exception {
    File file = new File("src/main/resources/books.csv");
    List<String> expectedLines = Lists.newArrayList("Being A Great Cook","Art is Fun","Be an Architect","History of Football","Gardening My Way");
    List<String> readLines = Files.readLines(file, Charsets.UTF_8,new ToListLineProcessor());
    assertThat(expectedLines,is(readLines));
}
```
