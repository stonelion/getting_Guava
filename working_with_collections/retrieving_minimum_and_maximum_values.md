# Retrieving minimum and maximum values
最后，让我们看看Ordering是怎样让我们轻松的从collection上取回最小或最大值。
```
Ordering<City> ordering = Ordering.from(cityByPopluation);
List<City> topFive = ordering.greatestOf(cityList,5);
List<City> bottomThree = ordering.leastOf(cityList,3);
```
我们从CityByPopulation comparator上建立Ordering实例。然后，我们调用`greatestOf`方法。这个方法会返回 n 个最大的元素。(例子上会返回5个)。`leastOf`有相同的参数，但是执行相反的动作，返回n个最小的元素。(例子上会返回3个)。
greatestOf和leastOf方法同样接受`Iterable<T>`接口。Ordering同样也可以取回最大或最小值。
