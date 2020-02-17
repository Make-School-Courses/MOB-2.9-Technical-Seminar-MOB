<!-- .slide: data-background="./Images/header.svg" data-background-repeat="none" data-background-size="40% 40%" data-background-position="center 10%" class="header" -->
# Sorting Algorithms

<!-- Put a link to the slides so that students can find them -->

➡️ [**Slides**](/MOB-2.9-Technical-Seminar-MOB/Slides/binarySearchTrees.html ':ignore')

<!-- > -->

## Learning Objectives

By the end of this lesson, you should be able to...

1. Review how to implement sorting algorithms
1. Practice interview questions with sorting methods

<!-- > -->

## O(n²) Sorting Algorithms

- Space efficient
- Favorable for small data sets
- Comparison based sorting methods

<!-- > -->

## Bubble sort

Compares adjacent values and swaps them if needed.

**Demo with whiteboards [8, 4, 10, 2]**

Completes when you can do a full pass over the collection without swapping values.

Worst case: n-1 passes (n = number of elements in the collection)

<!-- > -->

## Implementation

```swift
func bubbleSort<T>(_ array: inout [T]) where T: Comparable {
  guard array.count >= 2 else {
    return
  }
  for end in (1..<array.count).reversed() {
    var swapped = false
    for current in 0..<end {
      if array[current] > array[current + 1] {
        array.swapAt(current, current + 1)
        swapped = true
      }
    }
    if !swapped {
      return
    }
  }
}
```

Try it with the example from before. `bubbleSort(&array)`

<!-- > -->

## Selection Sort

- Same idea as bubble sort.
- Reduces the number of swaps.
- Will only swap at the end of each pass.

<!-- > -->

**Demo with whiteboards [8, 4, 10, 2]**

On each pass, find the lowest unsorted value and swap into place.

<!-- > -->

## Insertion Sort

- The more data already sorted, the less work needed to be done.
- Will iterate once through the cards, left to right. Each card is shifted to the left until it reaches the correct position.
- Fast if data is already sorted.

**Demo with whiteboards [8, 4, 10, 2]**


## Activity

Some of you implement selection sort, and others insertion sort. Pick yours 😯

```swift
func selectionSort<T>(_ array: inout [t]) where T: Comparable {}
```
```swift
func insertionSort<T>(_ array: inout [t]) where T: Comparable {}
```
<!--
func selectionSort<T>(_ array: inout [T])
    where T: Comparable {
  guard array.count >= 2 else {
    return
  }
  for current in 0..<(array.count - 1) {
    var lowest = current
    for other in (current + 1)..<array.count {
      if array[lowest] > array[other] {
        lowest = other
      }
    }
    if lowest != current {
      array.swapAt(lowest, current)
    }
  }
}

func insertionSort<T>(_ array: inout [T])
    where T: Comparable {
  guard array.count >= 2 else {
    return
  }
  for current in 1..<array.count {
    for shifting in (1...current).reversed() {
      if array[shifting] < array[shifting - 1] {
        array.swapAt(shifting, shifting - 1)
      } else {
        break
      }
    }
  }
}
-->

<!-- > -->

## Merge Sort

- Efficient sorting algorithm.
- O(n log n)
- Divide and conquer
- Split first, merge after

<!-- > -->

**Demo with whiteboards [7, 2, 6, 3, 9]**

<!-- > -->

## Implementation

```swift
func mergeSort<T>(_ array: [T])
    -> [t] where T: Comparable {
  let middle = array.count / 2
  let left = Array(array[..<middle])
  let right = Array(array[middle...])
  // ...
}
```
<aside class="notes">
Split array into halves. But this needs to happen recursively until we can't split anymore. Update this to have it split recursively.
</aside>

<!--
func mergeSort<T>(_ array: [T]) -> [T] where T: Comparable {
  guard array.count > 1 else {
    return array
  }
  let middle = array.count / 2
  let left = mergeSort(Array(array[..<middle]))
  let right = mergeSort(Array(array[middle...]))
  // ...
}
-->

<!-- > -->

## Implement Merge

Merge left and right arrays in a separate function.

```swift
func merge<T>(_ left: [t], _ right: [T]) -> [T] where T: Comparable {}
```

<!--
func merge<T>(_ left: [T], _ right: [T])
    -> [T] where T: Comparable {
  var leftIndex = 0
  var rightIndex = 0
  var result: [T] = []
  while leftIndex < left.count && rightIndex < right.count {
    let leftElement = left[leftIndex]
    let rightElement = right[rightIndex]
    // 4
    if leftElement < rightElement {
      result.append(leftElement)
      leftIndex += 1
    } else if leftElement > rightElement {
      result.append(rightElement)
      rightIndex += 1
    } else {
      result.append(leftElement)
      leftIndex += 1
      result.append(rightElement)
      rightIndex += 1
    }
  }
  if leftIndex < left.count {
    result.append(contentsOf: left[leftIndex...])
  }
  if rightIndex < right.count {
    result.append(contentsOf: right[rightIndex...])
  }
  return result
}
-->

<!-- > -->

## Complete mergeSort

```swift
func mergeSort<T>(_ array: [T]) -> [T] where T: Comparable {
  guard array.count > 1 else {
    return array
  }
  let middle = array.count / 2
  let left = mergeSort(Array(array[..< middle]))
  let right = mergeSort(Array(array[middle...]))
  return merge(left, right)
}

let array = [7, 2, 6, 3, 9]
print("Original: \(array)")
print("Merge sorted: \(mergeSort(array))")”
```

## [**10m**] BREAK

<!-- > -->

## Interview Challenge #1 - from Data Structures and Algorithms in Swift

Reverse a collection of elements by hand. Do not rely on the reverse or reversed methods.

<!-- > -->

## Interview Challenge #2 - from Data Structures and Algorithms in Swift

Write a function that takes two sorted arrays and merges them into a single array.
