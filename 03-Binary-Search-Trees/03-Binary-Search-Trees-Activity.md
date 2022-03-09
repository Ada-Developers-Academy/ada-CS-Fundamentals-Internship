# Activity:  Binary Search Trees

## Goal

Our goal is to practice using and manipulating `TreeNode` objects.

## Review Binary Search Trees Lesson

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: checkbox
* id: e2bae5b6-597a-4f7d-b8c2-1bf859ef2ad2
* title: Where are Binary Search Trees useful?
* points: 1
* topics: binary-search-trees, big-o

##### !question

What are advantages of a balanced Binary Search Tree?

##### !end-question

##### !options

* Fast insertion speed `O(log n)`
* Fast removal speed `O(log n)`
* Uses less space than a Linked List or Array
* Fast O(1) lookup speed
* Fast O(1) insertion to the head and tail
* Maintains the order of elements

##### !end-options

##### !answer

* Fast insertion speed `O(log n)`
* Fast removal speed `O(log n)`
* Maintains the order of elements

##### !end-answer

##### !hint

Remember that finding things in a balanced binary search tree is essentially performing binary search. Trees do have to maintain references to the children of each parent node.

This is also our first nonlinear data structure.

##### !end-hint

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: 9e97d43a-8b79-4577-9397-8739678fd1b8
* title: What is the height of the tree illustrated below?
* points: 1
* topics: python, binary-search-trees

##### !question

What is the height of the tree illustrated below?

![Unbalanced Binary Search Tree](./images/unbalanced-bst.png)

##### !end-question

##### !options

* 1
* 2
* 3
* 4
* 5

##### !end-options

##### !answer

* 5

##### !end-answer

##### !explanation

The max number of nodes you can travel through on a single path is 5.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->


### !challenge

* type: paragraph
* id: e7fd45e2-ec6a-4208-9682-8766406cb43f
* title: Why is it important for a tree to be balanced?
* points: 1
* topics: python, binary-search-trees

##### !question

Why is it so important for a Binary Search Tree to be balanced?

##### !end-question

##### !placeholder

Why keep a tree balanced?

##### !end-placeholder

##### !explanation

A Binary search tree maintains O(log n) time to find, add, and remove elements, *if and only if* the tree is balanced.  If the tree is not balanced then the time to find, add, and remove elements will resemble a be O(n).

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: paragraph
* id: 68fae9d7-dbd0-487f-8d18-0c6ba1ddc8aa
* title: Explain in your own words

##### !question

In your own words, why are Binary Search Trees useful?

##### !end-question

##### !placeholder

Why BSTs?

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Livecode - Project Introduction

As a class we will check out  the [project](./02-Bst-checkpoint.md) and work through a couple of the methods.  The purpose is to gain familiarity with the project and to learn how to write Binary Search Tree code.

Walkthrough with:

- Constructor
- Add Node (recursive & Iterative)
- Inorder Traversal

### Leetcode Style Question

In the next activity we will examine deleting a node in a BST.

- [Delete Node](https://replit.com/@adadev/bst-practice-delete#README.md)

Use drawings to illustrate the 4 scenarios.

1.  The Tree is empty (root is None).
    - return None
1.  The node to delete is the root
    - Insert the right subtree into the left subtree
    - Return the left subtree
1.  The node to delete is less than the root
    - root.left = delete_node on left subtree
1.  The node to delete is greater than the root
    - root.right = delete_node on right subtree


## Activity - Group Work Linked List Methods

- [Activity Replit](https://replit.com/@adadev/bst-practice#binary_search_trees/kth_smallest.py)

### Getting Started

In small groups of 3-4, **one student** will *fork* the given replit and then share a collaboration link with the rest of the team.

### Exercise

As a team complete the method in the replit.

If you finish early, you can depart the session or work on the project, with instructor support available.

### !callout-success

## Pay Attention to the InOrder Traversal

Could you use the inorder traversal to help you solve the problem?

### !end-callout

### !callout-secondary

## Suggestion:  Start The Project Now

It can be a *really* good idea to start the project with classmates and instructional staff around to ask questions of. Getting a solid start to a project makes the entire thing go easier.

### !end-callout