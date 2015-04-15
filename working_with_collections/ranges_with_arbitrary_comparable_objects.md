# Ranges with arbitrary comparable objects
因为Range对象可以使用任何实现`Comparable`接口的对象。很容易建立一个过滤器，来过滤那些可以落入到我们指定边界内的对象。看看这个Person类：
```
public class Person implements Comparable<Person> {
    private String firstName;
    private String lastName;
    private int age;
    private String sex;

    @Override
    public int compareTo(Person o) {
        return ComparisonChain.start().
        compare(this.firstName,o.getFirstName()).
        compare(this.lastName,o.getLastName()).
        compare(this.age,o.getAge()).
        compare(this.sex,o.getSex()).result();
    }
```

我们可以为`Person`的 `age`属性在35和50之间，建立一个Range实例。但是，如果我们看下compareTo方法就会发下一些问题；它包括类所有的属性。要解决这个问题，需要Range对象实现`Predicate`接口。

此外，我们还需要使用`Predicates.compose`方法来建立新的组合Range和Function的Predicate。首先，让我们定义Range实例：
```
Range<Integer> ageRange = Range.closed(35,50);
```

接下来，我们建立接受Person对象，返回age的 Function：
```
Function<Person,Integer> ageFunction = new                  Function<Person,Integer>() {
        @Override
        public Integer apply(Person person) {
            return person.getAge();
        }
};
```
最后，我们建立组合的Predicate：
```
Predicate<Person> predicate = Predicates.compose(ageRange,ageFunction);
```
现在，我们可以容易的建立一个`Predicate`实例来校验age的range。但是，通过组合，我们可以用新的Range对象代替，也可以用新的Comparable对象代替。
