# Immutable collections
目前为止，我们建立的collection都是可变的。然而，如果我们确实并不修改集合中的元素，那么我们应该使用不可变集合。首先、不可变集合完全是线程安全的。其次，对未知用户访问到代码提供了一层保护。