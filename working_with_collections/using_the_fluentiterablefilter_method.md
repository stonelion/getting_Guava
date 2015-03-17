# Using the FluentIterable.filter method
`FluentIterable.filter`方法使用`Predicate`作为参数。之后每一个元素都被检查，如果给定的`Predicate`检查元素返回true则会保留这个元素。如果没有对象满足`Predicate`，则会返回一个空的`Iterable`。下面的例子中，展示使用`from`和`filter`方法：
```
@Before
public void setUp() {
    person1 = new Person("Wilma", "Flintstone", 30, "F");
    person2 = new Person("Fred", "Flintstone", 32, "M");
    person3 = new Person("Betty", "Rubble", 31, "F");
    person4 = new Person("Barney", "Rubble", 33, "M");
    personList = Lists.newArrayList(person1, person2, person3,person4);
}

@Test
public void testFilter() throws Exception {
    Iterable<Person> personsFilteredByAge= FluentIterable.from(personList).filter(new Predicate<Person>() {
        @Override
        public boolean apply(Person input) {
            return input.getAge() > 31;
        }
    });
    assertThat(Iterables.contains(filtered,is(true));
    assertThat(Iterables.contains(filtered,is(true));
    assertThat(Iterables.contains(filtered,is(false));
    assertThat(Iterables.contains(filtered,is(false));
```
`setUp`方法内，我们建立一个通过调用Lists.newArrayList()静态工厂方法建立持有四个对象的`personList`。然后在`testFilter`方法内，我们建立`personsFilteredByAge`，通过传递`personList`为参数给`FluentIterable.from`方法，再使用`Predicate`为`filter`方法的参数组成过滤链。
在asserThat语句中，使用`Iterables.contains`方法来验证结果。`Iterables`是一个处理`Iterable`实例的工具类。
