# Ordered Collections of Data Review

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=ceac4982-192f-44a7-88a8-ad91016c972b&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

Students should be able to:

- Compare a Binary Tree to a Linked List
- Explain how a Binary Search Tree differs from a generic Binary Tree
- Write methods to perform the following on a Binary Search tree:
  - Search
  - Insert value
  - Delete value
  - Find height
  - Perform traversals including: 
    - Depth first traversals: pre-order, in-order, post-order
    - Breadth first traversal

## Video Lesson & Exercises

- [Video Lesson](https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=d9746397-8a10-43be-b1cc-aaaf00720b31)
- [C16 Slide Deck](https://docs.google.com/presentation/d/1Fj0deIUswGZ3ooJMpgVUqPEaWHKTkQ1w2Ci-yf8v66M/edit#slide=id.p)
- [BST Exercise](https://github.com/ada-c17/Sorted-Array-to-BST)

## Overview

We commonly encounter problems which require us to maintain ordered collections of data. This could be a list of students by name, jobs to process by priority or a collection of accounts by username.

When dealing with an ordered collection of data, we need to consider the time and space complexity of the following operations:

* **Insertion** - Adding elements to the collection
* **Deletion** - Removing elements from the collection
* **Searching** - Finding an element in the collection
* **Serialization** - Converting the collection to an array or string to write to a file, network, or database

Arrays and linked lists are two data structures that can be used to store ordered collections of data. Each has its respective advantages and disadvantages. 

### !callout-info

## What about dictionaries?

Dictionaries are unordered and thus cannot be used to store ordered data.

### !end-callout


### Review: Using An Array for Ordered Data

If we maintain an ordered array of data we can examine these 4 operations.

**Insertion** - O(n)

Adding an element to a sorted list requires us to first find the index in which to insert the new value and then each subsequent item must be shifted before a new item can be inserted.

Finding an item is an O(log n) operation because we can use [binary search](https://www.geeksforgeeks.org/python-program-for-binary-search/) to find the index to insert into.  Then shifting each element over to the right is an O(n) operation. Because the larger operation dominates, insertion is an O(n) operation.

![Adding an element to a sorted array](images/adding-sorted-array-element.png)

<!-- Image source:  https://www.draw.io/#G1j_vbvEN5UgNSszrKSPgwA7agvgQdhs1r -->

### !callout-info

## Binary Search v Binary Search Trees

Note that _binary search_ is different than a _binary search tree_. Binary search is an algorithm that can be used to find an element in a sorted array. A binary search tree is a type of tree structure which maintains special properties.

### !end-callout

**Deletion** - O(n)

Similar to insertion, removing an element from an ordered array requires first finding the index of the element to delete and then shifting each subsequent element over to the left.

![Deleting an element from an array](images/deleting-array-element.png)

<!-- Image at:  https://drive.google.com/file/d/1PeYa3z7mgVxy6jOPqS7brL09u2Vq_nFW/view?usp=sharing -->

**Searching** - O(log n)

To find an element in an ordered array, we can also use binary search.  Binary search is an O(log n) operation, therefore finding an element in an ordered array is also an O(log n) operation.

**Serialization** - O(n)

Serialization is the process of converting the data into a format that can be stored in a file, network, or database. In languages like Python this is often done by converting the data into a string.  You can do so using the [`JSON.dumps()`](https://www.geeksforgeeks.org/json-dumps-in-python/) function.  This function iterates through the list and converts each element into a string. This is an O(n) operation.

### Review: Using a Linked List for Ordered Data

We could also use a linked list. Linked lists perform slightly differently for the following operations.

**Insertion** - O(n)

Maintaining a linked list in order requires our application to:

1. **find** the location in the list to do the insertion - O(n)
2. Adjust the `next` pointers of the surrounding nodes to insert the new node - O(1)

While adjusting the surrounding links to insert a new node in a linked list is O(1), finding the location to do the insertion is O(n). So while the process of inserting a new node between two existing nodes in a linked list is very fast, finding the location to insert into is not, resulting in an overall O(n) operation.

**Deletion** - O(n)

Again deleting a specific node from a linked list requires us to first **find** the node. To find the node we must traverse the list until we find the node prior to the node we want to delete.  This is an O(n) operation.

**Searching** - O(n)

Because we cannot perform a binary search on a linked list, we must instead perform a linear search which runs in O(n) time.

**Serialization** - O(n)

To convert a linked list into a string or other data type suitable for writing to another device, we need to iterate through the list and access the value of each node. To visit each node requires O(n) operations and thus linear runtime.

## The Need

If at all possible, we want to maintain an ordered collection of data and outperform both arrays and linked lists in terms of insertion, deletion, searching and serialization.

The key requirements are:

1. Maintain a list of items in order.
2. Add and delete elements in better than O(n) time
3. Find elements with an O(log n) time
4. Serialize the list into a string or another data type that can be written to a file, network, or database in O(n) time or better.

If need 1 & 2 are maintained, an array will struggle to add and delete items. A linked list will require O(n) for all 4 operations because it has to traverse the sorted list to do anything.

A new data structure, a *binary search tree*, offers us a solution.


