# Writing to files
When working with input/output streams, there are several steps we have
to follow, which are:
1. Opening the input/output stream.
2. Reading bytes into or out of the stream.
3. When done, ensure all resources are properly closed in a finally block.
When we have to repeat this process, over and over again, it is error prone and
makes the code less clear and less maintainable. The Files class offers convenience
methods for writing/appending to a file or reading the contents of a file into a byte
array. Most of these become one-liners with the opening and closing of resources
being taken care of for us.
