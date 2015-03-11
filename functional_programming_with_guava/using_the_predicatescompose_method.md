# Using the Predicates.compose method
`Predicates.compose`方法接受`Function`和`Predicate`作为参数，对给定的`Predicate`实例计算基于从`Function`返回的值。

下面的例子上，我们准备建立一个新的`Predicate`:
```
public class SouthwestOrMidwestRegionPredicate implements
    Predicate<State> {
        @Override
        public boolean apply(State input) {
            return input.getRegion().equals(Region.MIDWEST) ||
            input.getRegion().equals(Region.SOUTHWEST);
        }
    }
```
下面，我们复用州查询`Function`来建立一个根据`Function`返回的州是否是位于中西或者西南部分。
```
Predicate<String> predicate =
Predicates.compose(southwestOrMidwestRegionPredicate,lookup);
```
