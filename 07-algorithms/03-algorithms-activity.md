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
* title: 1st iteration of QuickSort?
* points: 1
* topics: divide-and-conquer

##### !question

The [QuickSort]() algorithm takes an unsorted list, selects a specific element as a "pivot" and then partitions the list placing elements smaller than the pivot to the left of the pivot and elements larger than the pivot to the right of the pivot.  Then Quicksort is called recursively on the left and right partitions.

What type of Algorithm is Quicksort?


##### !end-question

##### !options

* `Divide and Conquer`
* `Greedy`
* `Dynamic Programming`
* `Exponential`

##### !end-options

##### !answer

Notice that Quicksort breaks the list into two smaller lists and sorts each of those lists.  This is a Divide and Conquer algorithm.

##### !end-answer

##### !hint

We are breaking the larger list into two smaller lists and sorting each.

##### !end-hint

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: 0bd5d043-4e3a-4281-85fa-bc5afb5b650e
* title: A Stack performs in a ______ manner.
* points: 1
* topics: stacks

##### !question

A stack performs in a ______ manner.

##### !end-question

##### !options

* First-In-First-Out (FIFO)
* Last-In-First-Out (LIFO)
* Hash-Table

##### !end-options

##### !answer

* Last-In-First-Out (LIFO)

##### !end-answer

##### !explanation

With a stack, the last item added is the first item removed.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: paragraph
* id: 921e7cf9-f423-4574-912f-ca1cec39159e
* title: Why would a circular buffer be useful to implement a queue?
* points: 1
* topics: python, queues, circular-buffer

##### !question

In your own words, why would a circular buffer be useful to implement a queue?

##### !end-question

##### !placeholder

Why use a circular buffer in a queue?

##### !end-placeholder

##### !explanation

A circular buffer maintains O(1) insertion and removal time complexities and maintains all the elements in an array for quick transfer to external media.  The elements are not fragmented across memory like in a linked list.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Livecode - Project Introduction

As a class we will check out  the [project](./02-stacks-and-queues-checkpoint.md) and work through the `enqueue` method.  The purpose is to gain familiarity with the project and to learn how to interact with a circular buffer.

Walkthrough with:

- Constructor
- enqueue

### Leetcode Style Question

Next we can try to use a stack to solve a LinkedList problem.

In this problem we need to:

1. Split the linked list into two halves
1. Reverse the second half (using a stack)
1. Merge the two halves together as a single interleaved linked list

**Exercise:**

- [Reorder Linked List](https://replit.com/@adadev/reorderlinkedlist#README.md)

## Activity - Group Work - Daily Temperatures

- [Activity Replit](https://replit.com/@adadev/Daily-Temperatures#README.md)

### Getting Started

In small groups of 3-4, **one student** will *fork* the given replit and then share a collaboration link with the rest of the team.

### Exercise

As a team complete the method in the replit.  There is a suggested solution in the `README.md` file. As a team read through the description and discuss how to implement the solution.

Then try to implement the solution as a team.

If you finish early, you can depart the session or work on the project, with instructor support available.

### !callout-secondary

## Suggestion:  Start The Project Now

It can be a *really* good idea to start the project with classmates and instructional staff around to ask questions of. Getting a solid start to a project makes the entire thing go easier.

### !end-callout