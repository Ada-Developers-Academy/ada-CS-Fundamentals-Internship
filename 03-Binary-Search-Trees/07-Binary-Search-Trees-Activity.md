# Activity:  Problem Solving

## Goal

Our goal is to practice using and manipulating `TreeNode` objects.

## Review Binary Search Trees Lesson

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: checkbox
* id: e2bae5b6-597a-4f7d-b8c2-1bf859ef2ad2
* title: Where are Binary Search Trees
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
* id: ca15bd85-d63b-4197-8a44-5caeecec1b54
* title: Explain in your own words

##### !question

In your own words, why are Binary Search Trees useful?

##### !end-question

##### !placeholder

Why BSTs?

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Livecode - Breadth First Search (BFS)

As a class we will walk through an implementation of Breadth First Search.

If you would like to follow along the live code, you can fork the Repl here: [Breadth First Search](https://replit.com/@adadev/bst-dfs-practice#binary_search_trees/bfs.py)

### Breakout Rooms - Depth First Search (DFS)

In small groups of 3-4 students, you will work to implement inorder, preorder, and postorder traversals of a BST. 

**One student** should *fork* the following Repl and share the collaboration link with the rest of the team. [BST Activity Repl](https://replit.com/@adadev/bst-dfs-practice#binary_search_trees/dfs.py)


#### Exercise

As a team complete the pre-order, in-order, and post-order methods in the replit.

If you finish early, you can take an early break or get started on the project with instructor support in the main room available.

