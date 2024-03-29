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

## Queue

We need to create a generic `Queue` interface using a generic type of Any just like we did in `Stack` basic structure.

```kotlin
interface Queue<T : Any> {

  val count: Int

  fun peek() : T?
  fun enqueue(element : T) : Boolean
  fun dequeue() : T?
  fun isEmpty() : Boolean
}
```

Now, we can create a new Queue class implementing the interface.

```kotlin
class QueueImplementation<T:Any> : Queue<T> {

  private var elements = arrayListOf<T>()
  override val count: Int = elements.size

  override fun enqueue(element: T) : Boolean {
    return elements.add(element)
  }

  override fun dequeue(): T? {
    return if (isEmpty()) null else elements.removeAt(0)
  }

  override fun peek(): T? {
    return elements.getOrNull(0)
  }

  override fun isEmpty(): Boolean {
    return count == 0
  }
}
```

***Note***: this implementation will work; however, implementing a `Queue` with normal Lists could be a performance issue due to eliminating the first element cause a copy operation to the other elements one position. One possible solution could be implementing this structure using `LinkedList` in order to avoid this `O(n)` operation.
