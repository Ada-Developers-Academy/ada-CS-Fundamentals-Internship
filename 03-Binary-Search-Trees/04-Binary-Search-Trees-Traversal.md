# Traversals

## Serialization

To serialize a tree, we need to traverse the tree.  This means we need to visit each node and add it to a string or array. There are several ways to do this.

A _traversal_ is an action visiting each node in a data structure such as a tree.  There are several kinds of traversals, Breadth First Traversals which visit each node level, by level and Depth First Traversals which visit a node's children before it's siblings.


### Depth First Traversals

Unlike linear data structures like arrays or linked list which have only one logical way to traverse them, trees can be traversed in different ways.  In a _depth first traversal_ you explore the children, grandchildren, and any further descendants of a node before moving to its sibling and traversing the sibling's descendants.

There are three standard types of depth-first traversals:

- **Pre-Order**:  Current, Left, Right
- **In-Order**: Left, Current, Right
- **Post-Order**: Left, Right, Current

In a **Pre-Order** traversal you execute the algorithm in this manner:

```
visit the current node
traverse the left subtree
traverse the right subtree
```

In a **In-Order** traversal you execute the algorithm in this manner:

```
traverse the left subtree
visit the current node
traverse the right subtree
```

In a **Post-Order** traversal you execute the algorithm in this manner:

```
traverse the left subtree
traverse the right subtree
visit the current node
```

Notice that all of the algorithms are recursive in structure because each node can be treated as it's own subtree.

![Binary Search Tree 2](images/bst2.png)

For the above Binary Search Tree
- **Pre-Order**:  [50, 25, 10, 30, 75, 60, 100]
- **In-Order**: [10, 25, 30, 50, 60, 75, 100]
- **Post-Order**: [10, 30, 25, 60, 100, 75, 50]

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: number
* id: 83e29c11-66b7-4b74-a85b-4fe936c92fa2
* title: Height of a tree
* decimal: 0
* points: 1
* topics: bst

##### !question

![bst3](images/bst3.png)

What is the height of the above BST?

##### !end-question

##### !placeholder

Number goes here

##### !end-placeholder

##### !answer

3
##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: a1703f9c-c97c-4b7a-86cf-cadb8780c77f
* title: Balanced
* points: 1
* topics: bst

##### !question

![bst3](images/bst3.png)

Is the tree balanced?

##### !end-question

##### !options

* Yes
* No
* Huh?

##### !end-options

##### !answer

* Yes

##### !end-answer

##### !hint

In a balanced tree no sibling subtrees differ in height more than 1.  So no left-right subtrees differ in height by 1.

##### !end-hint

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: e755df96-56ec-4d50-a336-3834838abb96
* title: Inorder
* points: 1
* topics: bst, traversal

##### !question

![bst3](images/bst3.png)

In what order would you hit the nodes doing an inorder traversal

##### !end-question

##### !options

* [17, 14, 20, 19, 52]
* [14, 17, 19, 20, 52]
* [14, 19, 52, 20, 17]

##### !end-options

##### !answer

* [14, 17, 19, 20, 52]

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: 08e94a48-fc15-4d95-8a47-d8ed9e199b34
* title: Preorder
* points: 1
* topics: bst, traversal

##### !question

![bst3](images/bst3.png)

In what order would you hit the nodes doing an preorder traversal

##### !end-question

##### !options

* [17, 14, 20, 19, 52]
* [14, 17, 19, 20, 52]
* [14, 19, 52, 20, 17]

##### !end-options

##### !answer

* [17, 14, 20, 19, 52]

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: c6009e6c-5717-459a-ae66-4570918271b9
* title: Postorder
* points: 1
* topics: bst, traversal

##### !question

![bst3](images/bst3.png)

In what order would you hit the nodes doing an postorder traversal

##### !end-question

##### !options

* [17, 14, 20, 19, 52]
* [14, 17, 19, 20, 52]
* [14, 19, 52, 20, 17]

##### !end-options

##### !answer

* [14, 19, 52, 20, 17]

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### Why Do Traversals

Traversals can be very useful to serialize our data structure into a format that can be easily read by humans or stored on another device.

- **Pre-order** If we need to save a tree data structure to disk, or send it across the network and maintain the structure, pre-order traversals can be useful.
- **In-Order**: If we need to print or otherwise visit all the nodes of a tree in order.
- **Post-Order**: If we need to delete all the nodes in a BST.

### !callout-info

## Why are they all left-to-right?

So why are all the traversals left-to-right instead of right-to-left?

Computer Science was initially pioneered in western cultures where people read left-to-right and so their cultural bias lead to designing traversals in that manner.  There's no inherent characteristics of binary search trees which require a left-to-right traversal.  You could create a right-to-left traversal, but for historical reasons, these are the standard binary search tree traversals.

### !end-callout

## Breadth First Search Traversal

A breadth first search traversal, like depth first search traversals, begins at the root node of the tree. It then examines each node level by level, meaning the root's direct children are examined, then the root's grandchildren, and so on and so forth.  

To implement breadth first search, we use a [queue](../02-linked-lists/04-linked-lists-stacks-queues.md), which is a linear ordered collection of data which adds and removes elements according to a first-in first-out (FIFO) principle similar to a queue or line of people in real life: the first element added to the queue is the first to be removed from the queue.

Pseudocode for the algorithm is as follows:

```
Create an empty queue
Create an empty list to store the explored nodes

Add the root into the queue

While the queue is not empty:
    Pop the next node off the queue and add its children to the queue
    Add the popped node to the list of explored nodes
```

### !callout-info

## Deque

[`deque`](https://docs.python.org/3/library/collections.html#collections.deque) from the `collections` module is commonly used to create queues in Python. 

### !end-callout

## Serialization Big O

Serialization algorithms are O(n) in both time and space complexity. Both breadth first search and depth first search algorithms visit each node in the array exactly once, giving O(n) time complexity where n is the number of nodes in the tree. They also both create an array to store each explored node giving O(n) space complexity.

If we were to just perform a traversal using either breadth first or depth first search without storing the explored nodes in an array or other auxiliary data structure, the space complexity would be slightly different.

With depth first search algorithms, we need to consider how many recursive calls would be on the call stack at any given time. The maximum number of recursive calls would be the height of the tree since depth first search algorithms go as deep as they can into the tree before turning back and exploring other subtrees. So we can say the space complexity is O(h) where h is the height of the tree.

With breadth first search, we need to consider the maximum number of nodes that would be in our queue at any given time. Since breadth first search adds all the nodes in a level to the queue before starting to pop them off, the space complexity would be O(b) where b is the breadth (the number of nodes on the level with the greatest number of nodes) of the tree.

## Summary

In the lesson, we examined different methods to traverse a tree.  Unlike a linked list where there is only one possible traversal method, a tree has multiple ways to traverse.
