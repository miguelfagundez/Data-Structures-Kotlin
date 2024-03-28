# Data-Structures-Kotlin
Basic data structures implementation in Kotlin

## Stack

We can create a generic `Stack` interface using a generic type of Any.

```kotlin
interface Stack<T : Any> {

  val count: Int

  fun pop() : T?
  fun push(element : T)
  fun peek() : T?
  fun isEmpty() : Boolean
}
```

Now, we can create a new Stack class implementing the interface.

```kotlin
class StackImplementation<T:Any> : Stack<T> {

  private var elements = arrayListOf<T>()
  override val count: Int = elements.size

  override fun pop(): T? {
    return elements.removeLastOrNull()
  }

  override fun push(element: T) {
    elements.add(element)
  }

  override fun peek(): T? {
    return elements.lastOrNull()
  }

  override fun isEmpty(): Boolean {
    return count == 0
  }
}
```
