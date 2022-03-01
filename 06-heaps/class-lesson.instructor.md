# Lesson Plan

Heaps/priority queues are a data structure which is less essential to interviewing than trees, maps, stacks, queues and linked lists.  That said, priority queues are a very useful data structure in many applications.  They are used to implement a variety of algorithms, including Dijkstra's Algorithm.

Heaps could be swapped out for another topic, if the replacement is felt to be more important.

## Lesson Goals

We want students to:

- Be able to map an array to a tree structure with the `left_child = 2 * i + 1` and `right_child = 2 * i + 2` formulas.
- Be able to explain the operations of a heap including insertion and removal.
- Be able to implement a heap data structure.
- Be able to identify places in code to use a heap and to use a heap in a coding problem.

## Before Class

1. Review the [heapq](https://docs.python.org/3/library/heapq.html) module.
1. Review the replits for solutions.

## Review Hash Tables Project - 10 minutes

Start off the lesson by welcoming students to the class and note attendance. You can use the Airtable to record attendance The [C16 Airtable](https://airtable.com/appkfPQ769uxQLSei/tbl6oiA8ZG1wKUonM/viwgf4wesbLFMlg1L?blocks=hide) is linked.

Take a moment to review any questions from Hash Tables and allow students to present their solutions.

### !callout-info

## Students may not want to do this

Students can be a bit shy, but you can contact specific students ahead of time asking them to be ready to present, "because you find their solution interesting."  Being prepared helps with student confidence.

### !end-callout

## Heaps Introduction - 10 minutes


Then follow the 1st part of the [activity](./03-Heaps-Activity.md) reviewing the data structure. 

Specifically reinforce:

- How to map an array to a tree data structure and the formula to find left & right children (as well as parents)
- How an element is inserted into a heap
- How an element is removed from a heap
- Uses for a heap

## Livecode - 20 minutes

In the livecode walk through the `add` methdo to the project and pseudocode the `heap_up` helper method.

Remember to:

- Try to get students to navigate as you type.  
- Cause a bug, and try to promote student ideas to fix it.
- Model how to use the tests and print statements.

Then:

1. Walk through the `heapq` module
    - Have students read the docs for the functions and answer the questions on the activity
    - Compare that solution to the project
    - Write a couple of coding examples
1. Livecode the [Find K Pairs with Smallest Sums](https://replit.com/@adadev/Find-K-Pairs-with-Smallest-Sums-Solution) problem with students illustrating the uses for a priority queue.
    - Ask, "Why could a priority queue make sense here?"

## Coding Activity - 60 minutes

Break students into breakout rooms to practice the replit. Optionally you can talk through some pseudocode before students start working.

Iterate through the breakout rooms answering questions as you go.

## Solution Examples

Solutions:

- [Solution to the project](https://github.com/adagold/heaps/tree/python-solution)
- [Solution to Merge K Sorted LIsts](https://replit.com/@adadev/Merge-K-Sorted-Lists-Solution)