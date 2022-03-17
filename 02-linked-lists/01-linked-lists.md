# Linked Lists

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=b1664c7e-f95e-40f5-971f-ad9000fe85d8&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Video Lesson

- [Slides](https://docs.google.com/presentation/d/1UKi2M_V5wgIC9K_xfmtdBmeKokdKep1gRcnz0vLXNHk/edit?usp=sharing)
- [Linked List Exercises](https://github.com/Ada-C16/linked-list)

## Learning Goals

By the end of this lesson students should be able to:

- Describe the structure of a singly linked list, and doubly linked list
- Compare and contrast the a advantages and disadvantages of singly and doubly linked lists.
- Implement an Object Oriented Singly Linked List
- Write methods to perform a variety of tasks on a singly linked list

## Overview

An Array is an ordered, linear collection of data where each element sits next to the previous element.  Because each element is of uniform size, and adjacent to it's neighboring elements, with some basic math, the interpreter or compiler can jump to any element in the array immediately.  The interpreter takes the memory address of the 1st element of the array and adds the size of each element plus the index number of the sought element.  

![ Array ](images/array.png)

A Linked List is also a linear collection where one element is first, another second etc, but each element instead contans a _reference_ to the next element in the list.  In that manner you could say that an element _points_ to the next item.  A Linked List forms a series of nodes linked together like a chain in memory.  

![Linked List Image](images/singly-linked-list.png)
<!-- Image from https://en.wikipedia.org/wiki/Linked_list -->

### Singly Linked Lists

A Singly Linked List is the most basic form of a Linked List.  The data structure maintains a reference, typically called `head` which references the first node in a list.  That node maintains a field, typically called `next`, which reference the next node etc.  The last node in a linked list, sometimes called the `tail`, has `null` or `nil` as it's `next` reference.  

![Singly Linked List](images/singly-linked-list2.png)

<!-- image from https://www.geeksforgeeks.org/difference-between-a-static-queue-and-a-singly-linked-list/ -->

### Doubly Linked Lists

A Doubly Linked List extends this by adding a `previous` reference to each node.  That `previous` reference points to the prior node.  The `head` node's `previous` field will be `nil` or `null`.

![Doubly Linked List](images/doubly-linked-list.png)

## Advantages & Disadvantages

You can use a doubly or singly linked list in any place you could use an array, but they have specific advantages depending on the use-case.

Doubly linked lists take up additional memory, due to the additional references, but it is possible to iterate through in reverse, and it can be a little easier to sort or add/remove elements in the middle of the list more easily.

### Over Arrays

Both Arrays & Linked Lists are linear data structures and both have a clearly defined order with first and last elements.  An array however has the ability to use an _index_ to select any element in constant time, while to find an arbitrary element in a linked list requires you to start at the head and iterate through the links until you find the element.  You can visualize and explore linked list operations on [visualgo.net](https://visualgo.net/en/list).

Big-O For Linked Lists & Arrays

| Operation  | Linked Lists  |  Array  |
|--- |--- |--- |
| access | O(n) | O(1) |
| search | O(n) | O(n) |
| insertion | O(1) | O(n) |
| deletion | O(1)  | O(1) |

As you can see above, Linked Lists perform in constant time to insert values into or remove values from a list, because it only requires a few reference to be changed.  Arrays, on the other hand, can require shifting numerous elements into new indices with each insertion or deletion.

Further most runtimes allocate more memory to an array than is being used because if the array grows, the interpreter needs to request new memory from the environment and copy the entire array into the new, larger, space.  By starting with extra space available an array can grow as required for some time.  A LinkedList by contrast only uses memory as required for the nodes available.  An array also requires each element to be adjacent in memory.  When available memory is limited, this can be problematic.  So in some memory restrictive environments a Linked List could be attractive.  

Linked Lists have the following advantages:

- **Dynamic Size** Linked Lists are of dynamic size, a Linked List only uses the memory required for it's current nodes.
- **Insertion/Deletion** Because each element does not need to be adjacent in a LinkedList it is easier to insert or remove element by adjusting the links, O(1).  
  - Arrays require shifting adjacent elements on insertion or deletion, O(n).

Arrays have the following advantages:

- **Random Access** Using by using the index you can quickly access any element in an array, O(1).  A Linked List requires you to traverse the list until you find the element, O(n).
- **No next/previous References** Each node in a Linked List requires, at least, a reference to the next node.  This is an additional complication and a bit of extra memory usage.
- **Caching** Because the memory is colocated, it's easier to move an array into faster system cache memory.

### Questions

<!-- 
<details>
<summary>You need to regularly add orders to the end of a list and remove orders from the front to process them.  What would you pick, LinkedList or Array?</summary>
  
A Linked List because you can add and remove elements from the ends in constant time O(1) vs an Array where you have to shift all elements over causing it to run in O(n) time.
</details>
-->

<!--
<details>
<summary>You need to regularly look up students from an unordered list and remove them from the list.  What would you pick a LinkedList or an Array?</summary>
  
Either could work as finding an element will take O(n) for an unordered list in both cases.  Granted removing an element in a LinkedList will take O(1) vs O(n) for an Array.
</details>
-->

## Object Oriented Design of a Linked List

### Encapsulation

When designing a data structure like a Linked List, we typically design the data structure as abstract, hiding implementation.  So the designer could switch a LinkedList into an ArrayList without impacting user functionality.  They could also transition into a DoublyLinkedList without impacting users.  

### Node Class

The node class encapsulates each element of the LinkedList..  It provides an attribute to store data and a node referencing the next node in the chain.  It provides an interface for our LinkedList to deal with the data and connect nodes.

```python
# Defines a node in the singly linked list
class Node:
    def __init__(self, value):
        self.data = value
        self.next = None
```

![Linked List Node](images/nodeLinkedList.png)

### Linked List Class

```python
# Defines the singly linked list
class LinkedList:
    def __init__(self):
        self.head = None

    # Method. Adds a new node with the specific data value to the beginning of the linked list.
    def add_first(self, value):
        new_node = Node(value)

    # Method. Returns the value in the first node in the linked list.
    # Returns None if the list is empty.
    def get_first(self):
        pass

    # Method. Returns the value of the last node in the linked list. Returns None if the list is empty.
    def get_last(self):
        # Return None if the list is empty
        # Otherwise, traverse the list to the end
        # Then return the last node's value
        pass

    # Method. Returns the value at a given index in the linked list.
    # Index count starts at 0.
    # Returns None if there are fewer nodes in the linked list than the index value.
    def get_at_index(self, index):
        # Traverse the list
        # <index> times
        # or until the end is reached
        # Then return the current node's value
        pass
```

### Adding A Node

Adding a node to the front of the LinkedList class above is relatively straightforward.  You:

- Create a new Node
- Make the new node's next field be the current `head` of the list
- Set the `head` to become the new node

Step 1:

![add-first-1](images/add-first-1.png)

Step 2:

![add-first-2](images/add-first-2.png)

Step 3:

![add-first-3](images/add-first-3.png)

Step 4:

![add-first-4](images/add-first-4.png)

```python
def add_first(self, value):
    new_node = Node(value)
    new_node.next = self.head
    self.head = new_node
```

### Removing a node at a specific index

To remove a node at a specific index, you first have to traverse the list until you find the index before the node to delete.  If the node to remove is the head, then the head becomes the next element.  Then adjust the prior node's `next` reference to point **past** the node you are removing.  

![remove a node #1](images/remove-node-1.png)
![remove a node #2](images/remove-node-2.png)
![remove a node #3](images/remove-node-3.png)
![remove a node #4](images/remove-node-4.png)

```python
def remove(self, index):
    if not self.head:
        return

    if index == 0:
        self.head = self.head.next

    # Traverse the list until you find the node at index -1
    current = self.head
    current_index = 0
    while current.next and current_index < index - 1:
        current = current.next
        current_index += 1

    # If the node exists
    if current.next:
        current.next = current.next.next
```

## Supplemental Concepts

### Pointers & References

You will often hear the terms _pointer_ and _reference_ in relation to dynamic data structures like LinkedLists.  Both terms refer to a variable which **points** to data in memory, or holds the address of another varaible in memory.  The concept is similar to a home.  The home is an object in memory, while the home's address is a _reference_ which indicates where to find the home.

In some languages like C/C++ you can manipulate memory addresses and memory directly.  In other languages, like Python, you have references which refer to objects in memory, but you cannot directly work with the memory addresses.

An example in C++

```c++
  int x = 5;
  int *ptr_x;
  ptr_x = &x;  // Assign ptr_x the value of the memory address of x.
```

We use references in Python whenever we use a Linked List since each node _refers_ to the next node in the chain and `head` refers to the 1st node in the chain.

![Singly Linked List](images/singly-linked-list2.png)

### Memory Leaks

Is a bug in how a program manages memory.  A _memory leak_ occurs when memory that is no longer needed by the program is not released back to the operating system.  Over time, if memory is used, and not returned to the system less and less memory is available to other programs and eventually not enough memory is available to run applications.  Modern operating systems return all system memory allocated to a program when it ends.  Thus memory leaks in long-running processes like daemons can cause a system to run out of memory.

In Python, the Python interpreter manages memory for developers.  Python uses a [garbage collection](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)) system which identifies memory no longer used by the application and returns it.

Consider when a node is removed from a Linked List:

![Removing a node](images/linked-list-remove-node.png)
<!-- source:  https://stackoverflow.com/questions/41474163/singly-linked-list-remove -->

When no variable refers to a node (holding 99 in the image above) the Python garbage collector will eventually return the memory to the operating system.

```python
def remove_first(self):
    if not self.head:
        return False

    value = self.head.value
    self.head = self.head.next

    return value
```

Some languages however, place memory management on the developer.  C is one such language.  These lower-level languages give a developer more flexibility and control over low-level operations, at the cost of more responsibility and a greater likelyhood of errors.

Removing a Node from a Linked List in C

```c
void removeFirst(struct node **headRef) {
  if (*head != NULL) {
    struct node* temp = *head;
    int value = (*temp)->value;
    head = (*head)->next;
    free(temp);  // <-- Give back memory to the OS
    return value;
  }
}
```

## Challenge Problem

### !challenge

- type: code-snippet
- id: aadddd4b-2b3d-4c47-8f38-ec8f24f91d90
- language: python3.6
- title: Merge Two Sorted Linked Lists
- points: 1
- topics: python, linked-list, interview-problem-easy

##### !question

Write a `sorted_merge()` function that takes two lists, each of which is sorted in increasing order, and merges the two together into one list which is in increasing order. `sorted_merge()` should return the new list. The new list should be made by splicing together the nodes of the first two lists.

Example input and output:
| input | output |
|--|--|
|`list_a = 5->13->15` <br> `list_b = 6->9->20` | `5->6->9->13->15->20`|

There are many cases to deal with:

- Either `a` or `b` may be empty initially
- During processing either `a` or `b` may run out first

You may be destructive with the original two lists.

##### !end-question

##### !placeholder

```py
class ListNode:
    def __init__(self, value, next = None):
        self.value = value
        self.next = next
    
    def __repr__(self):
        return f"ListNode({self.value})"
    def __str__(self):
        answer = []
        current = self
        while current is not None:
            answer.append(f"{current.value}")
            current = current.next
        
        return "->".join(answer)

def sorted_merge(list_a, list_b):
    '''
    INPUT: list_a: the head reference of a sorted linked list
            list_b: the head reference of a sorted linked list
    OUTPUT: the head reference of a sorted linked list that is the result of merging list_a and list_b
    '''
    pass
```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestSortedMerge(unittest.TestCase):
    def test_two_empty_lists(self):
        # Arrange
        list_a = None
        list_b = None
        # Act
        result = sorted_merge(list_a, list_b)

        # Assert
        self.assertEqual(result, None)

    def test_one_empty_list(self):
        # Arrange
        list_a = ListNode(1)
        list_a.next = ListNode(2)
        list_b = None
        # Act
        result = sorted_merge(list_a, list_b)

        # Assert
        self.assertEqual(result.__str__(), "1->2")
    
    def test_another_one_empty_list(self):
        # Arrange
        list_b = ListNode(1)
        list_b.next = ListNode(2)
        list_a = None
        # Act
        result = sorted_merge(list_a, list_b)

        # Assert
        self.assertEqual(result.__str__(), "1->2")

    def test_one_short_one_long_list(self):
        # Arrange
        list_a = ListNode(1)
        list_a.next = ListNode(6)
        list_b = ListNode(5)
        list_b.next = ListNode(10)
        list_b.next.next = ListNode(15)
        # Act
        result = sorted_merge(list_a, list_b)

        # Assert
        self.assertEqual(result.__str__(), "1->5->6->10->15")

    def test_one_long_one_short_list(self):
        # Arrange
        list_b = ListNode(1)
        list_b.next = ListNode(6)
        list_a = ListNode(5)
        list_a.next = ListNode(10)
        list_a.next.next = ListNode(15)
        # Act
        result = sorted_merge(list_a, list_b)

        # Assert
        self.assertEqual(result.__str__(), "1->5->6->10->15")
    

    def test_two_longish_lists(self):
        # Arrange
        list_a = ListNode(1)
        list_a.next = ListNode(6)
        list_a.next.next = ListNode(27)
        list_a.next.next.next = ListNode(30)
        list_b = ListNode(5)
        list_b.next = ListNode(10)
        list_b.next.next = ListNode(15)
        list_b.next.next.next = ListNode(29)
        # Act
        result = sorted_merge(list_a, list_b)

        # Assert
        self.assertEqual(result.__str__(), "1->5->6->10->15->27->29->30")
```

##### !end-tests

##### !hint

This is actually quite similar to [merging two sorted arrays](https://www.geeksforgeeks.org/merge-two-sorted-arrays/).  The only difference is that the two lists are linked lists.

##### !end-hint

### !end-challenge

[Problem Source: mycodeschool](https://www.youtube.com/user/mycodeschool)

## Resources

- [Linked Lists from Geeks for Geeks](https://www.geeksforgeeks.org/data-structures/linked-list/) - Lots of articles & practice problems
- [Stanford LinkedList Basics](http://cslibrary.stanford.edu/103/LinkedListBasics.pdf)
