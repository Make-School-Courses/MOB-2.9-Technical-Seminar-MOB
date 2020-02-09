<!-- .slide: data-background="./Images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# Stacks

<!-- Put a link to the slides so that students can find them -->

<!-- pg 72, pg 327 -->

➡️ [**Slides**](/MOB-2.9-Technical-Seminar-MOB/Slides/trees.html ':ignore')

<!-- > -->

## Learning Objectives

By the end of this lesson, you should be able to...

1. Review how to implement trees and their methods
1. Practice interview questions that use trees

<!-- > -->

## Trees

A tree is a data structure used to solve challenges with:
- hierarchical relationships
- sorted data
- wanting fast lookup operations

<!-- > -->

## Nodes

Trees are made up of nodes. Each node:
- Holds data
- Keeps track of its children

![nodes](assets/nodes.png)

<!-- > -->

## Parent/Child

We view trees starting from the top and branching towards the bottom. (The opposite of a real tree)

- All nodes except for the one at the top are connected to exactly one node above. This is the parent node.

- The nodes below the parent are its child nodes.

![parentchild](assets/parentchild.png)

<!-- > -->

## Root

The node at the top is called the **root** of the tree.

![root](assets/root.png)

<!-- > -->

## Leaf

A **leaf** is a node without children.

![leaf](assets/leaf.png)

<!-- > -->

## Create the tree node class

1. Open a playground and add a `TreeNode` class.

2. Remember each node holds a value and its children (use an array).

3. Include the method to add a child.

<!--
class TreeNode<T> {
    var value: T
    var children: [TreeNode] = []

    init(_ value: T) {
        self.value = value
    }
    func add(_ child: TreeNode) {
        children.append(child)
    }
}
-->

<!-- > -->

## An example

Try your new class

```swift

let animals = TreeNode("Animals")
let vertebrates = TreeNode("Vertebrates")
let invertebrates = TreeNode("Invertebrates")
animals.add(vertebrates)
animals.add(invertebrates)
```

Draw the graphical representation of the tree so far.

<!-- > -->

## Iterating through trees

The traversal strategy you choose depends on the problem that you want to solve.

**Depth-first-travelsal** is a technique that starts at the root and visits nodes as deep as it can before backtracking.

<!--
func forEachDepthFirst(visit: (TreeNode) -> Void) {
       visit(self)
       children.forEach {
           $0.forEachDepthFirst(visit: visit)
       }
   }
-->

<!-- > -->

## Implement depth-first traversal.

You can use recursion to process the next node.

Test is out by extending the original tree to this:

![animals](assets/animals.jpg)

And then calling your traversal method.

<!-- > -->

<!--
func makeAnimalsTree() -> TreeNode<String> {
    let tree = TreeNode("Animals")

    let vertebrates = TreeNode("Vertebrates")
    let invertebrates = TreeNode("Invertebrates")

    let reptiles = TreeNode("Reptiles")
    let birds = TreeNode("Birds")
    let fish = TreeNode("Fish")
    let amphibians = TreeNode("Amphibians")

    let protzoa = TreeNode("Protzoa")
    let flatworms = TreeNode("Flatworms")
    let coelenterates = TreeNode("Coelenterates")
    let worms = TreeNode("Worms")
    let echinoderms = TreeNode("Echinoderms")
    let molluscs = TreeNode("Molluscs")

    let arthropods = TreeNode("Arthropods")

    let arachnids = TreeNode("Arachnids")
    let crustaceans = TreeNode("Crustaceans")
    let insects = TreeNode("Insects")
    let myrapods = TreeNode("Myrapods")

    tree.add(vertebrates)
    tree.add(invertebrates)

    vertebrates.add(reptiles)
    vertebrates.add(birds)
    vertebrates.add(fish)
    vertebrates.add(amphibians)

    invertebrates.add(protzoa)
    invertebrates.add(flatworms)
    invertebrates.add(coelenterates)
    invertebrates.add(arthropods)
    invertebrates.add(worms)
    invertebrates.add(echinoderms)
    invertebrates.add(molluscs)

    invertebrates.add(arthropods)

    arthropods.add(arachnids)
    arthropods.add(crustaceans)
    arthropods.add(insects)
    arthropods.add(myrapods)

    return tree
}

let tree = makeAnimalsTree()
tree.forEachDepthFirst { print($0.value) }

-->

<!-- > -->

## Level-Order Traversal

We visit each node of the tree based on the depth of the nodes.

```swift
func forEachLevelOrder(visit: (TreeNode) -> Void) {
  visit(self)
  var queue = Queue<TreeNode>()
  children.forEach { queue.enqueue($0) }
    while let node = queue.dequeue() {
      visit(node)
      node.children.forEach { queue.enqueue($0) }
    }
}
```

Write down the result from calling this method on the current tree.

<!-- > -->

## Write a search method

Now that we know how to iterate through the tree, write a search method to find a node.

Test it with the following:

```swift
if let result = tree.search("Insects") {
    print(result.value)
} else {
    print("Not found")
}
```

<!--
extension TreeNode where T: Equatable {
    func search(_ value: T) -> TreeNode? {
        var result: TreeNode?
        forEachLevelOrder { node in
            if node.value == value {
                result = node
            }
        }
        return result
    }
}
-->

<!-- > -->

<!-- .slide: data-background="#087CB8" -->

## [**10m**] BREAK

<!-- > -->

## Interview Challenge #1 - from Data Structures and Algorithms in Swift

Print the values in a tree in an order based on their level. Nodes belonging in the same level should be printed in the same line.

Example:
![treechallenge](assets/treeChallenge.png)

Output:
15<br>
1 17 20<br>
1 5 0 2 5 7

Helper Queue:
```swift
public struct Queue<T> {

  private var leftStack: [T] = []
  private var rightStack: [T] = []

  public init() {}

  public var isEmpty: Bool {
    return leftStack.isEmpty && rightStack.isEmpty
  }

  public var peek: T? {
    return !leftStack.isEmpty ? leftStack.last : rightStack.first
  }

  public private(set) var count = 0
  @discardableResult public mutating func enqueue(_ element: T) -> Bool {
    count += 1
    rightStack.append(element)
    return true
  }

  public mutating func dequeue() -> T? {
    if leftStack.isEmpty {
      leftStack = rightStack.reversed()
      rightStack.removeAll()
    }

    let value = leftStack.popLast()
    if value != nil {
      count -= 1
    }
    return value
  }
}
```
