# CacheLoader
CacheLoaders是一个抽象类，因为load方法是抽象的。 There is also a loadAll method that takes an
Iterable object, but loadAll delegates this Iterable object to load for each item
contained in the Iterable object (unless we've overridden the loadAll method).
There are two static methods on the CacheLoader class that will allow us to leverage
some of the constructs we have learned about from Chapter 3, Functional Programming
with Guava. The first method is shown as follows:
CacheLoader<Key,value> cacheLoader =
CacheLoader.from(Function<Key,Value> func);
Here we can pass in a Function object that will transform an input object into
an output object. When used as an argument of the CacheLoader.from method, we
get a CacheLoader instance where the keys are the input objects to Function and the
resulting output objects are the values. Similarly, we also have the second method
shown as follows:
CacheLoader<Object,Value> cacheLoader =
CacheLoader.from(Supplier<Value> supplier);
In this preceding example, we are creating a CacheLoader instance from a Supplier
instance. It's worth noting here that any key passed to CacheLoader will result in the
Supplier.get() method being called. There is an implied assumption with both of
these methods that we are re-using existing Function or Supplier instances and not
creating new objects simply for the sake of creating CacheLoader.
