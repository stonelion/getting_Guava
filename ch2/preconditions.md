# Preconditions
`Preconditions`类是用于检查我们代码状态的静态方法集合。
`Preconditions`是十分重要的，因为它保证代码像我们所期望的那样成功地执行。如果所检查的条件不符合我们期待的那样，那么就可以立即回馈问题出现在哪里。

当然你也写出属于自己的`preconditions`,例如：
```
    if(someObj == null){
        throw new IllegalArgumentException(" someObj must not be null");
    }
```
通过使用`preconditions`(静态导入)，我们可以更简洁的检查参数是否为null。
```
    checkNotNull(someObj,"someObj must not be null");
```

接下来，来看看preconditions的一个例子：
```
public class PreconditionExample {
    private String label;
    private int[] values = new int[5];
    private int currentIndex;

    public PreconditionExample(String label) {
        //returns value of object if not null
        this.label = checkNotNull(label,"Label can''t be null");
    }

    public void updateCurrentIndexValue(int index, int valueToSet) {
        //Check index valid first
        this.currentIndex = checkElementIndex(index, values.length,"Index out of bounds for values");
        //Validate valueToSet
        checkArgument(valueToSet <= 100,"Value can't be more than 100");
        values[this.currentIndex] = valueToSet;
    }

    public void doOperation(){
        checkState(validateObjectState(),"Can't perform operation");
    }
    private boolean validateObjectState(){
        return this.label.equalsIgnoreCase("open") && values[this.currentIndex]==10;
    }
}
```

- `checkNotNull (T object, Object message):` 当object为非空的时，这个方法返回object；否则，抛出NullPointerException错误。

- `checkElementIndex (int index, int size, Object message):`这个方法中，index变量的值是你要尝试访问的元素位置，并且size变量的值是某个集合的长度。若index在范围之内则返回所引用的对象，相反抛出`IndexOutOfBoundsException`错误。

- `checkArgument (Boolean expression, Object message):` 这个方法计算一个入参状态的Boolean表达式。这个表达式期望的值是true，否则的话会抛出`IllegalArgumentException`。

- `checkState (Boolean expression, Object message):`这个方法计算一个对象状态的Boolean表达式。而不是参数的。这个表达式期望的值是true，否则的话会抛出`IllegalArgumentException`。

