# InputSupplier and OutputSupplier
Guava has InputSupplier and OutputSupplier interfaces that are used as suppliers of InputStreams/Readers or OutputStreams/Writers. We'll see in the following section how these interfaces benefit us, as Guava will typically
open, flush, and close the underlying resources when these interfaces are used.
