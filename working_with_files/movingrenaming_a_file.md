# Moving/renaming a File

```
public class GuavaMoveFileExample {
    public static void main(String[] args) {
        File original = new File("src/main/resources/copy.txt");
        File newFile = new File("src/main/resources/newFile.txt");
        try{
            Files.move(original, newFile);
        }catch (IOException e){
            e.printStackTrace();
        }
    }
}
```
例子中，我们使copy.txt重命名为newFile.txt。
