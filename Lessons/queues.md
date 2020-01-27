<!-- .slide: data-background="./Images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# Queues

<!-- Put a link to the slides so that students can find them -->

➡️ [**Slides**](/MOB-2.9-Technical-Seminar-MOB/Slides/queues.html ':ignore')

<!-- > -->

## Learning Objectives

By the end of this lesson, you should be able to...

1. Review how to implement queues and their methods
1. Practice interview questions that use queues

<!-- > -->

## Queue

Queues use FIFO.

The first item added to the queue will be the first to be removed.

Use queues when it's important to keep the ordering of elements to process later.

<!-- > -->

```swift
public protocol Queue {
  associatedtype Element
  mutating func enqueue(_ element: Element) -> Bool
  mutating func dequeue() -> Element?
  var isEmpty: Bool { get }
  var peek: Element? { get }
}
```

<!-- > -->

## Queue operations

- **enqueue:** Adds an element at the back of the queue. Returns true if it was successful.

- **dequeue:** Removes the element at the front of the queue and returns it.

- **isEmpty:** Checks if the queue is empty.

- **peek:** Returns the element at the front of the queue.

<!-- > -->

## Analysis

|       | push | append | insert after | node at |
|:-----:|:----:|:------:|:------------:|:-------:|
|action |      |        |              |         |
|time complexity |      |              |         |

<!-- > -->

## Activity in pairs

Add the removing operations in the linked list.

- **pop:** Removes the first node.
- **removeLast:** Removes the last node.
- **remove(at:):** Removes a value at a specific index

```swift
@discardableResult public mutating func pop() -> T? {

}

@discardableResult public mutating func removeLast() -> T? {

}

@discardableResult public mutating func remove(after node: Node<T>) -> T? {

}
```
<!--
Solution:
@discardableResult public mutating func pop() -> T? {
        defer {
            head = head?.next
            if isEmpty {
                tail = nil
            }
        }
        return head?.value
    }

    @discardableResult public mutating func removeLast() -> T? {
        guard let head = head else {
            return nil
        }
        guard head.next != nil else {
            return pop()
        }
        var prev = head
        var current = head
        while let next = current.next {
            prev = current
            current = next
        }
        prev.next = nil
        tail = prev
        return current.value
    }

    @discardableResult public mutating func remove(after node: Node<T>) -> T? {
      defer {
        if node.next === tail {
          tail = node
        }
        node.next = node.next?.next
      }
      return node.next?.value
    }
-->

<!-- > -->

## Analysis

|       | pop | removeLast | remove after |
|:-----:|:----:|:------:|:---------------:|
|action |      |        |                 |         
|time complexity |      |                 |         

<!-- > -->

<!-- .slide: data-background="#087CB8" -->
## [**10m**] BREAK

<!-- > -->

## Interview Challenge #1 - from Data Structures and Algorithms in Swift

Given a linked list as your input, write a function that prints the nodes in reverse order. You should not use recursion to solve this problem.


<!-- v -->

## Interview Challenge #2 - from Data Structures and Algorithms in Swift

Given a linked list, write a function that returns the middle node.

```
1 -> 2 -> 3 -> nil
// return 2

1 -> 2 -> 3 -> 4 -> nil
// return 3

```

<!-- v -->

## Interview Challenge #3 - from Data Structures and Algorithms in Swift

Write a function that takes 2 sorted linked lists and merges them into one.

```
1 -> 5 -> 8 -> 10
0 -> 2 -> 6 -> 11

//merges into

0 -> 1 -> 2 -> 5 -> 6 -> 8 -> 10 -> 11
```

<!-- v -->

## Interview Challenge #4 - from Data Structures and Algorithms in Swift

Write a function that removes all occurrences of a given element in a linked list.

```
1 -> 6 -> 8 -> 8 -> 4

// after removing all occurrences of 8
1 -> 6 -> 4
```

<!-- > -->

## Resources

Data Structures & Algorithms in Swift. By Matthijs Hollemans
