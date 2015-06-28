# Hashing a file
产生某个文件的Hash值。
```
public class HashFileExample {
    public static void main(String[] args) throws IOException {
    File file = new File("src/main/resources/sampleTextFileOne.txt");
    HashCode hashCode = Files.hash(file, Hashing.md5());
    System.out.println(hashCode);
    }
}
```
例子中，我们使用Files.hash方法，应用文件对象和HashFunction实例。
