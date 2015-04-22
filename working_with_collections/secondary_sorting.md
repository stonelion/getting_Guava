# Secondary sorting
通常在排序对象的时候，我们需要处理排序标准是相同的情况，并且需要定义第二个配需标准。上面章节中，我们定义了Comparator根据人口排序City对象，现在我们定义另外一个Comparator::

```
public class CityByRainfall implements Comparator<City> {
    @Override
    public int compare(City city1, City city2) {
        return Doubles.compare(city1.getAverageRainfall(),city2.getAverageRainfall());
    }
}
```

上面的代码中声明的Comparator会根据平均年降雨量排序City对象。则下面我们可以使用另一个Comparator。

```
Ordering.from(cityByPopulation).compound(cityByRainfall);
```

从CityByPopulation Comparator建立Ordering对象，然后调用compound方法。这个例子中，使用另一个CityByRainfall comparator。现在，当排序City对象有相同的人口数的时候，Ordering实例会委托给第二个comparator。

例子：
```
@Test
public void testSecondarySort(){

    City city1 = cityBuilder.population(100000).averageRainfall(55.0).build();
    City city2 = cityBuilder.population(100000).averageRainfall(45.0).build();
    City city3 = cityBuilder.population(100000).averageRainfall(33.8).build();

    List<City> cities = Lists.newArrayList(city1,city2,city3);
    Ordering<City> secondaryOrdering = Ordering.from(cityByPopulation).compound(cityByRainfall);

    Collections.sort(cities,secondaryOrdering);

    assertThat(cities.get(0),is(city3));
}
```
