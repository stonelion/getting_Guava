# Closer
用于保证调用Closer.close方法时，所有注册的Closeable对象都正确的关闭。

```
public class CloserExample {
    public static void main(String[] args) throws IOException {
    Closer closer = Closer.create();
        try {
        File destination = new File("src/main/resources/copy.txt");
        destination.deleteOnExit();
        BufferedReader reader = new BufferedReader(new FileReader("src/main/resources/sampleTextFileOne.txt"));
        BufferedWriter writer = new BufferedWriter(new FileWriter(destination));
        closer.register(reader);
        closer.register(writer);
        String line;

        while((line = reader.readLine())!=null){
            writer.write(line);
        }

        } catch (Throwable t) {
            throw closer.rethrow(t);
        } finally {
            closer.close();
        }
    }
}
```
