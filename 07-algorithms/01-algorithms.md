# Introduction to Algorithms

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=2619c3c1-e6d5-48a1-a199-aad7014dcc4e&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

**Note** This video lesson covers algorithms content as it was written for cohorts C16 and prior. Significant changes have been made, and the above videos do not fully align with the updated lesson content. However, they do provide a good general overview of divide and conquer, greedy, and dynamic programming for those who prefer video lessons.

## Learning Goals

By the end of this lesson you should be able to:

- Further explain time and space complexity
- Explain the term algorithm
- Explain three categories of algorithms _greedy_, _divide and conquer_ and _dynamic programming_

## Video Lesson

- [Slide Deck used for C16](https://docs.google.com/presentation/d/1V4ycrfl3dbL0IbRHqK3ytU45VyMJQNHhyxpc3Ti2e28/edit?usp=sharing)

## What is an an algorithm

So what is an algorithm?  An **algorithm** is a finite set of instructions that, if followed, accomplishes a particular task.  We can think of it as a series of steps to accomplish a task.  For example Google maps has an algorithm to calculate the best route to drive between any two points on map.  

All algorithms must have:

- Input
  - An algorithm may accept zero or more inputs
- Output
  - An algorithm should produce some result
- Clarity
  - Each step in an algorithm should be a clear and unambiguous
- Finiteness
  - An algorithm should end after a finite number of steps. 
  - An algorithm cannot repeat forever (otherwise it doesn't solve a problem)
- Effectiveness
  - It should be possible for a person or computer to fulfill each step in an algorithm and the algorithm should accomplish the given task.

The art of computer science is really the art of devising, analyzing, proving the correctness and testing algorithms.

### Algorithms areas of study

The study of computer science is the study of algorithms.  Researchers in CS focus on:

- **Devising** algorithms
  - This is the art of using data structures and design strategies to develop new and useful algorithms
  - It also encompasses optimizing and generalizing existing algorithms
- **Validating** algorithms
  - This is the art of proving the correctness of an algorithm for all possible inputs
  - This is very similar to a mathematical proof
- **Analyzing** algorithms
  - This is identifying the time and space complexity of an algorithm
- **Testing** algorithms
  - When we test an algorithm we are really debugging it.  
  - When we test an algorithm we run it on sample data and try to determine if it failed and if so correct the error.
  - We also _profile_ or conduct performance measurements by running the algorithm on sample data and measuring performance changes and memory usage.
    - If you have seen [leetcode](https://leetcode.com/), this site will take your solution to a common programming problem and compare it's performance to solutions from other developers.

## Analyzing Algorithms

When we analyze an algorithm we generally do not care how an algorithm performs on a specific input size.  Instead we look at how the runtime and memory usage changes as the input size grows.  Looking at how an algorithm's runtime and memory usage increases with increasing input is called, _Asymptotic Analysis_, i.e. Big O.

Why bother with asymptotic analysis?  Why bother with examining how an algorithm increases in runtime and memory usage as the input size increases?  Asymptotic analysis allows us to compare algorithms and select one over another.  It also allows us to judge if any algorithm will be able to solve a particular problem within a meaningful amount of time or the system's limited storage capacity.

Most often, we measure things in terms of _worst-case_ performance of an algorithm.  This is important when response time and memory usage is critical like in managing a self-driving car or autopilot system.  There are also times where the _average-case_ performance is important, especially where an algorithm is run often or across many instance, like an analysis program run regularly on a cloud platform. The average runtime (and standard deviation) can be important for a task run thousands of times an hour.

| Big-O | English Term
|--- |--- |
| O(1) | Constant |
| O(log n) | Logarithmic |
| O(n) | Linear |
| O(n<sup>2</sup>) | Quadratic |
| O(n<sup>3</sup>) | Cubic |
| O(2<sup>n</sup>) | Exponential |
| O(n!) | Factorial |

### Analyzing Binary Search Trees

In a _balanced_ binary search tree, finding a particular node has an asymptotic complexity of O(log<sub>2</sub> n), because at each step we cut the number of possible nodes by half.  This type of algorithm is called a **divide and conquer** algorithm and will be discussed in more detail further on in the lesson.

In this divide and conquer algorithm we:

- Divide by splitting the remaining nodes into a left and right subtrees
- Conquer by continuing the search on the subtree which may contain the element

In a divide and conquer algorithm we reduce a large problem into smaller subproblems, which are the same problem, but in a smaller scale until we reach a base-case.  In this example, when we reach the node being searched for or a leaf node.

Because we will continually divide our list of potential nodes in half until we reach a leaf node, or the item searched for, this algorithm is O(log n) for time complexity.

![Balanced Binary Search Tree](images/bst-divide-and-conquer.png)

### Mergesort

Mergesort is another classic divide and conquer algorithm.  In mergesort, if our list has a size greater than 1, we divide our list into two halves conduct a mergesort on each half and merge the sorted lists together.

![Example MergeSort Diagram](images/MergeSort.png)

#### Analysis of Mergesort

If the Time complexity of mergesort is `T(n)` we can determine the time complexity of mergesort as follows.

**Dividing** When we divide the list into two sublists this takes `O(1)` as it just calculates the middle of the sub-array.
**Conquer**  We then recursively sort each half, which is of size n/2.  You can then say that the time complexity of both halves is `2 * T(n/2)`.
**Combining** The merge method into an n-element subarray is `O(n)`.  

If you look at the diagram above we will divide and recombine a total of log n levels, just like a binary tree.  At each level of the merging step we will be merging a total of `n` elements.  Since we will have log n levels and at each level we merge n elements, this algorithm is `O(n log n)`

## Categories of Algorithms

There are a [number of different categories of algorithms](https://s2.smu.edu/~vdebroy/cse3353/Lectures/Lecture-7/Algorithm-Types.pdf).  Each category describes the general approach to the algorithm's use in solving its particular problem.  Categories are not exclusive; an algorithm can be a member of multiple categories.  For example QuickSort can be both a divide and conquer algorithm and a randomized algorithm if it picks a random element as a pivot to sort against at each stage.

In this lesson we will look at a few categories, specifically _divide and conquer_ algorithms, _greedy_ algorithms and _dynamic programming_ algorithms.


