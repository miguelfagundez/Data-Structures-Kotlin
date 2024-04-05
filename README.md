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

## Queue (List)

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

***Note***: this implementation will work; however, implementing a `Queue` with normal Lists could be a performance issue due to eliminating the first element cause a copy operation to the other elements one position. One possible solution could be implementing this structure using `Linked List` in order to avoid this `O(n)` operation.

## Queue (Linked List)

A linked list is a chain of nodes which have a value and a reference to the next node in the list. Now, we can create a node class:

```kotlin
data class Node<T:Any>(
  var value: T,
  var next: Node<T>? = null
)
```

The absence of a reference to the next node represents the end of the list (null). Now we can implement the `Queue` interface:

```kotlin
class QueueLinkedListImplementation<T:Any> : Queue<T> {

// head: it stores the front node of Linked List
  private var front: Node<T>? = null
// rear: it stores the last node of Linked List
  private var rear: Node<T>? = null
// number of elements in the queue
  private var count = 0

  override fun enqueue(element: T) : Boolean {
    try{
        // Create a new node
        var newNode = Node(element);
 
        // If queue is empty, then new node is, both, front and rear
        if (rear == null) {
            front = rear = newNode
            count++
            return true
        }
 
        // Add the new node at the end of queue and change rear
        rear.next = newNode;
        rear = newNode;
        count++
        return true
    }catch(exception: Exception){
      // if there is any problem, return false
      return false
    }
  }

  override fun dequeue(): T? {
    try{
        // If queue is empty, return null
        if (front == null){
            count == 0
            return null
        }
 
        // Store previous front and move front one node ahead
        var tempFront = front;
        front = front.next;
 
        // If front becomes null, then change rear also as null
        if (front == null)
            rear = null;

        count--
        return tempFront
    }cath(exception: Exception){
        // if there is any problem, return null
        return null
    }    
  }

  override fun peek(): T? {
    // Just returning first queue element if any, otherwise return null
    return front 
  }

  override fun isEmpty(): Boolean {
    return count == 0
  }
}
```

With this linked list implementation, we have only `0(1)` time complexity in enqueue and dequeue operations.
