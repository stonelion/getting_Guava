# Multimaps
虽然map是日常变成中主要用到的数据结构，但有时还是需要为给定key关联超过一个value。当然，我们可以自由的建立属于自己的以list或set作为值的map实现，但是，Guava让这简单。静态工厂方法返回的map实例，提供了相似的put(key,value)操作语义。实现的细节是，检查是否给定key存在`collection`，是否需要创建，然后添加值到`collection`中。让我们深入阐述这有用的抽象。
