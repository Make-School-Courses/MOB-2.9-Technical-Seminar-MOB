<!-- .slide: data-background="./Images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# Stacks

<!-- Put a link to the slides so that students can find them -->

<!-- pg 72, pg 327 -->

➡️ [**Slides**](/MOB-2.9-Technical-Seminar-MOB/Slides/stacks.html ':ignore')

<!-- > -->

## Learning Objectives

By the end of this lesson, you should be able to...

1. Review how to implement stack and their methods
1. Practice interview questions that use stacks

<!-- > -->

## Stacks: Waffles

When you think about a stack data structure, you can referene this stack of delicious waffles:

<img width="400px" src=assets/waffles.jpeg />

When you eat a stack of waffles, do you start from the bottom, or the top? If you were to add another waffle to your stack (you're really hungry) would you add to the bottom or the top?

<!-- v -->

## Stack Data Structures are the Same!

- When you add an item to the stack, you add it to the top
- When you remove an item from a stack, you always remove from the top
- This is what's known as **Last In First Out (LIFO)**, as the last item to enter the data structure will be the first one to leave it

<!-- v -->

## Question: Why Would We Use Stacks?

<p class="fragment fade-in">When you want to enforce a specific usage pattern (LIFO)</p>

<p class="fragment fade-in">When you want to get things out in the reverse order than you put them in</p>

<p class="fragment fade-in">navigation, memory allocation, finding a path out of a maze, backtracking, etc.</p>

<!-- > -->

## Stack Methods

**Essential Methods:**

- **push:** Takes an element as input and adds it to the top of the stack
- **pop:** Removes the element at the top of the stack and then returns it

**Non-essential Methods:**

- **peek:** Returns the element at the top of the stack, but does _not_ alter or change the stack
- **isEmpty:** Returns `True` if a stack is empty, and `False` if it is not

<!-- > -->

## Activity: Implementing a Stack 

Adapted from `Data Structures and Algorithms in Swift`.

Use the following starter code to implement a stack data structure. Note that the `storage` private variable will be used to hold the elements in the stack.

**Hint:** What other data structure could be useful here to help us implement our `Stack`?

```swift
public struct Stack<Element> {
    private var storage: //TODO
    
    public init() { }
      
    public mutating func push(_ element: Element) {
        //TODO
    }
      
    @discardableResult
    public mutating func pop() -> Element? {
        //TODO  
    }
    
    // Stretch Challenges: Implement the below functions
    public func peek() -> Element? {
        // TODO: solution should be 1 line
    }
    
    public var isEmpty: Bool {
      // TODO: solution should be 1 line
    }
}
```

<!-- v -->

## Review Solution

- First take 5 min to review with a partner and compare solutions
- After that, we will review the solution as a class

<!-- 
Solution:
public struct Stack<Element> {
    private var storage: [Element] = []
    
    public init() { }
      
    public mutating func push(_ element: Element) {
        storage.append(element)
    }
      
    @discardableResult
    public mutating func pop() -> Element? {
        return storage.popLast()
    }
    
    // Stretch Challenges: Implement the below functions
    public func peek() -> Element? {
        return storage.last
    }
    
    public var isEmpty: Bool {
      return peek() == nil
    }
}
-->

<!-- > -->

## Complexity Analysis

**Question:** What's the average runtime for the `push` method? _Justify your answer_

<p class="fragment fade-in">O(1)</p>

**Question:** What's the average runtime for the `pop` method? _Justify your answer_

<p class="fragment fade-in">O(1)</p>

_**You will always be asked to justify your answers in an interview!**_

<!-- > -->

<!-- .slide: data-background="#087CB8" -->
## [**10m**] BREAK

<!-- > -->

## Interview Challenge #1 - from Data Structures and Algorithms in Swift

Given a linked list as your input, write a function that prints the nodes in reverse order. You should not use recursion to solve this problem.


<!-- v -->

## Interview Challenge #2 - from Data Structures and Algorithms in Swift

Given a string, check if there are `(` and `)` characters, and return true if the parentheses in the string are balanced. For example:
```// 1
h((e))llo(world)() // balanced parentheses
// 2
(hello world // unbalanced parentheses
```

<!-- v -->

## Interview Challenge #3 - from Interview Cake

Use your Stack class to implement a new class `MaxStack` with a method `getMax()` that returns the largest element in the stack. `getMax()` should _not_ remove the item.


<!-- > -->

## Wrap Up

 - Stacks are a relatively simple data structure, best used when a LIFO usage pattern is needed
 - `push` and `pop` are the essential methods