# Activity:  Algorithms

## Goal

Our goal is to introduce types of algorithms and practice using dynamic programming.

## Review Heaps Project

We will start by reviewing student solutions to the [Heaps](../06-heaps/02-heaps-exercise-checkpoint.md) project.

- How did we implement `heap_up`?
- How did we implement `heap_down`?
- Did we use recursion?

## Review Algorithms Project

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: 512ee510-1a21-45c3-9ef9-4eee8f21ad11
* title: What type of algorithm is QuickSort?
* points: 1
* topics: divide-and-conquer

##### !question

The [QuickSort](https://www.geeksforgeeks.org/quick-sort/) algorithm takes an unsorted list, selects a specific element as a "pivot" and then partitions the list placing elements smaller than the pivot to the left of the pivot and elements larger than the pivot to the right of the pivot.  Then Quicksort is called recursively on the left and right partitions.

<details style="max-width: 700px; margin: auto;">

  <summary>See Quicksort Algorithm</summary>

  ```py
    # The main function that implements QuickSort
    def quick_sort(start, end, array):
     
    if (start < end):
         
        # p is partitioning index, array[p]
        # is at right place
        # O(n) time complexity for partition
        p = partition(start, end, array)
         
        # Sort elements before partition
        # and after partition
        quick_sort(start, p - 1, array)
        quick_sort(p + 1, end, array)
  ```

</details>

What type of Algorithm is Quicksort?


##### !end-question

##### !options

* `Divide and Conquer`
* `Greedy`
* `Dynamic Programming`
* `Exponential`

##### !end-options

##### !answer

* `Divide and Conquer`

##### !end-answer

##### !hint

We are breaking the larger list into two smaller lists and sorting each.

##### !end-hint

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: 85c94f42-7e79-4b10-8f0e-8fd1480db6d0
* title: What type of algorithm is this?
* points: 1
* topics: divide-and-conquer

##### !question

Consider the problem: 

```
Given a value V, if we want to make a change for V Rs, and we have an infinite supply of each of the denominations in Indian currency, i.e., we have an infinite supply of { 1, 2, 5, 10, 20, 50, 100, 500, 1000} valued coins/notes, what is the minimum number of coins and/or notes needed to make the change?
```

We could solve the problem with the following algorithm

1. Sort the array of coins in decreasing order.
1. Initialize result as empty.
1. Find the largest denomination that is smaller than current amount.
1. Add found denomination to result. Subtract value of found denomination from amount.
1. If amount becomes 0, then print result.
1. Else repeat steps 3 and 4 for new value of V.

What type of algorithm is this?

##### !end-question

##### !options

* `Divide and Conquer`
* `Greedy`
* `Dynamic Programming`
* `Exponential`

##### !end-options

##### !answer

* `Greedy`

##### !end-answer

##### !hint

We are breaking the larger list into two smaller lists and sorting each.

##### !end-hint

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: 83937a9d-feca-45b1-9dd3-9e3c6b5a94be
* title: Explain how this algorithm uses dynamic programming.
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
* topics: python, algorithms, dynamic-programming

##### !question

Below is an example of a Fibonacci program solution solving 

```
Fib(0) = 0
Fib(1) = 1
Fib(n) = Fib( n - 1) + Fib(n-2) for all n > 1
```

How does this algorithm use dynamic programming?

```py
def fib(n):
    fibs = [0, 1]
    for i in range(2, n + 1):
        fibs.append(fibs[i - 1] + fibs[i - 2])
    
    return fibs[n]
```

##### !end-question

##### !placeholder

Explain how this uses dynamic programming.

##### !end-placeholder

<!-- other optional sections -->
##### !hint

All dynamic programming solutions involve a "memo" or a cached solution to one or more subproblems and uses that memo to solve the larger problem.  Where is the memo?

##### !end-hint

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Livecode - Project Introduction

As a class we will check out  the [project](./02-algorithms-checkpoint.md) and work through the `Newman-Conway Sequence` function.

### Leetcode Style Question

Next we can try to use a stack to solve a dynamic programming problem.

In this problem we need to:  

1. Store a "memo" of all the substrings that exist in the string where if memo[3] is True the string from indicies 0->3 can be segmented by the words in the dictionary.
1. Iterate through the string from 1 to length + 1 using loop variable `i`
1. Then loop through the string from 0 to `i` using loop variable `j`
1. If the substring to index `j` is in the memo, and the substring from indicies j to i is in the dictionary, then update the memeo at index i and break to the next iteration of the outer loop.
1. After the loop return if the memo at the length of the string found a solution

**Exercise:**

- [Word Break](https://replit.com/@adadev/Word-break)

## Activity - Group Work - House Robber

- [Activity Replit](https://replit.com/@adadev/House-Robber#README.md)

### Getting Started

In small groups of 3-4, **one student** will *fork* the given replit and then share a collaboration link with the rest of the team.

### Exercise

As a team complete the method in the replit.  **There is a suggested Dynamic Programming solution in the `README.md` file. As a team read through the description and discuss how to implement the solution.**

Then try to implement the solution as a team.

If you finish early, you can depart the session or work on the project, with instructor support available.

### !callout-secondary

## Suggestion:  Start The Project Now

It can be a *really* good idea to start the project with classmates and instructional staff around to ask questions of. Getting a solid start to a project makes the entire thing go easier.

### !end-callout