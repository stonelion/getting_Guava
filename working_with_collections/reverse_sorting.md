# Reverse sorting
看下如下的Comparator实例，更具人口数量来对City对象排序。

```
public class CityByPopluation implements Comparator<City> {
    @Override
    public int compare(City city1, City city2) {
        return Ints.compare(city1.getPopulation(),city2.getPopulation());
    }
}
```
可以使用如下代码建立一个相反的Ordering对象。指定顺序是相反的，从最大到最小。
```
Ordering.from(cityByPopluation).reverse();
```
