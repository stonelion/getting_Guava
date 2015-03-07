# Generating hash code
为一个对象写`hashCode`经常的事情，当然也是一件乏味的事情。使用`Objects`类的`hashCode`方法，会让这件事更容易一些。

假设 `Book` 类有四个成员属性：title,author,publisher和isbn。

下面的例子展示了如何使用`Object.hashCode`方法:

```
public int hashCode() {
    return Objects.hashCode(title, author, publisher, isbn);
}
``
