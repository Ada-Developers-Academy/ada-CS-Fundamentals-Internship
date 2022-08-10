# Object Oriented Design of a Linked List

## Overview
In Python, linked lists are not a built-in data type. So how might we represent linked lists? Classes provide a mechanism for us to define our own linked list data type. 

Linked lists are a collection of nodes. A node is also a data structure that is not built in to Python. Thus, in order to represent a linked list, we will first want to define a Node class that represents a single element in a linked list. We can then define a LinkedList class that represents an ordered collection of individual Node objects. 

## Node Class

The Node class encapsulates each individual element of the linked list. It is comprised of an attribute that stores data and an attribute that stores the next node in the chain. It provides an interface for the LinkedList class we will create to handle the data and link nodes together.

```python
# Defines a node in the singly linked list
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None
```

![Linked List Node](images/nodeLinkedList.png)

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 4ed61105-fe6b-483d-9c54-83bd67414dee
* title: Doubly Linked List Node Class
* points: 1

##### !question

Above, we wrote the Node class constructor for a singly linked list. Alter the code below to write a Node class constructor for a doubly linked list.

##### !end-question

##### !placeholder

```py
```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
  def test_one(self):
    self.assertEqual(1,1)
```

##### !end-tests

##### !hint
In addition to the `value` and `next` attributes, nodes in a doubly linked list should also maintain a reference to the _previous_ node in the list.

##### !end-hint

d-rubric (markdown, instructors can see while scoring a 

##### !explanation 

An example of a working implementation:

```python
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None
        self.prev = None
```
You might also consider passing in default values for `next` and `prev`. 
##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## LinkedList Class

The LinkedList class has a single attribute `head` which stores a reference to the first node in the list. Our constructor initializes `head` to `None` so that when a new LinkedList is initialized, we are creating an empty list.  

The LinkedList class also has several methods which will allow users to perform operations on or pull information out of the linked list. Below we provide function stubs for several possible methods a LinkedList class may have. Other LinkedList classes may choose to extend this functionality with additional methods. For example, the designer could add a `reverse` method to reverse the linked list or a `search` method to find the first element with a specified value in the linked list.

```python
# Defines the singly linked list
class LinkedList:
    def __init__(self):
        self.head = None

    # Method. Adds a new node with the specific data value to the beginning of the linked list.
    def add_first(self, value):
        pass

    # Method. Returns the value in the first node in the linked list.
    # Returns None if the list is empty.
    def get_first(self):
        pass

    # Method. Returns the value of the last node in the linked list. Returns None if the list is empty.
    def get_last(self):
        pass

    # Method. Returns the value at a given index in the linked list.
    # Index count starts at 0.
    # Returns None if there are fewer nodes in the linked list than the index value.
    def get_at_index(self, index):c
        pass
```

### Adding A Node

Adding a node to the front of the LinkedList class above is relatively straightforward. The steps are as follows:

1. Create a new Node object
2.  Set the new node's next field to the current `head` of the list
3. Set the `head` to become the new node

We can visualize the above steps with this example linked list:

![add-first-1](images/add-first-1.png)

Step 1. Create a new Node object:

![add-first-2](images/add-first-2.png)

Step 2. Set the new node's next field:

![add-first-3](images/add-first-3.png)

Step 3. Set the head node as the new node:

![add-first-4](images/add-first-4.png)

We can write this method in Python as:

```python
def add_first(self, value):
    new_node = Node(value)
    new_node.next = self.head
    self.head = new_node
```

<!--TODO: Add challenge question adding node for a doubly linked list-->

### Encapsulation

When designing a data structure like a linked list, we typically want our design to include not just our linked nodes but also methods that operate on our linked list, such as methods to add nodes, delete nodes, or get the length of the linked list. Bundling together multiple pieces of data and methods that operate on that data is called __encapsulation__, and you may already be familiar with it in the form of classes. 

Encapsulation also enables us to design our data structure as __abstract__, meaning that the implementation of the data structure is hidden. This allows the internal implementation of the data structure to change without affecting user functionality. As a result, the designer could switch a linked list into an array list without the user needing to know. They could also transition from a singly linked list into a doubly linked list without impacting users. 

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: a9c61442-b23f-44c3-8b05-eae600e286dc
* title: implement get_first
* points: 1
* 
##### !question

Now that we have implemented `add_first` together, try implementing `get_first` on your own. `get_first` should return the value of the first node in the linked list. If the list is empty, `get_first` should return `None`. 

##### !end-question

##### !placeholder

```py
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    def add_first(self, value):
        new_node = Node(value)
        new_node.next = self.head
        self.head = new_node

    def get_first(self):
        #write your code here
        pass

```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_get_first_returns_none_for_empty_list(self):
        lst = LinkedList()
        self.assertEqual(None, lst.get_first())

    def test_get_first_returns_head_of_list_length_one(self):
        lst = LinkedList()
        lst.add_first(3)
        self.assertEqual(3, lst.get_first())

    def test_get_first_returns_head_of_list_length_two(self):
        lst = LinkedList()
        lst.add_first(3)
        lst.add_first(5)
        self.assertEqual(5, lst.get_first())
```

##### !end-tests

### !hint

`self.head` is the first node in the list!

Still feeling stuck? Check this video walkthrough of the solution.
<!-- TODO: Add video walkthrough to explanation -->

### !end-hint

### !explanation

An example of a working implementation:

```python
def get_first(self):
    if not self.head:
        return None
    return self.head.val
```

### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: e1b8f953-0850-4472-b775-d9c38fedbe83
* title: `get_first` Time Complexity
* points: 1

##### !question

What is the time complexity of `get_first`?

##### !end-question

##### !options

a| O(1)
b| O(log n)
c| O(n log n)
d| O(n)
e| O(n^2)

##### !end-options

##### !answer

a|

##### !end-answer


##### !explanation
The time complexity will be O(1) or constant as we are simply accessing an attribute of our linked list.

##### !end-explanation

### !end-challenge
<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: bea80606-a87d-4dd2-97d9-b0e7cb7afc91
* title: Space complexity `get_first`
* points: 1

##### !question

What is the space complexity of `get_first`?

##### !end-question

##### !options

a| O(1)
b| O(log n)
c| O(n log n)
d| O(n)
e| O(n^2)

##### !end-options

##### !answer

a|

##### !end-answer


##### !explanation
The space complexity will be O(1) or constant as we are not creating any new data structures or call stacks whose size are proportional to the length of our list.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### Traversing Linked Lists
Because linked lists are not stored in contiguous memory like arrays, most read and write operations will require us to traverse the list. With a singly linked list, we only maintain a reference to the `head` node, so all of our traversals will start at the `head` of the list.

Consider a `search` method which allows users to determine whether any nodes in the list have a specified value. The `search` method takes one parameter: a value to search for. The method should return `True` if a node with that value exists within 

We can break down the `search` method as follows:

- Create a current pointer and point it to the head of the list
- While there are nodes we haven't looked at yet:
  - Return `True` if the current node has the specified value
  - Otherwise, redirect current to reference the next node in the list
- Return `False` if we have looked at all nodes and still have not found any nodes that have the specified value

```python
   def search(self, value):
    current = self.head

    while current:
        if current.val == value:
            return True
        current = current.next
    
    return False
```

Creating a `current` pointer to help iterate through the nodes in a linked list is a useful strategy that cna be applied in many similar linked list applications.

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 18990a10-7a4a-4064-99f3-6a721aa851e8
* title: `get_at_index`
* points: 1

##### !question

Write a `get_at_index` method for a singly linked list that returns the value at a given index in the linked list. The index count should begin at 0 and the function should return `None` if there are fewer nodes in the linked list than the given index value.

##### !end-question

##### !placeholder
```py
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    def add_first(self, value):
        new_node = Node(value)
        new_node.next = self.head
        self.head = new_node

    def get_at_index(self, index):
        #write your code here
        pass
```

##### !end-placeholder

##### !tests
```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_get_at_index_is_none_with_empty_list(self):
        lst = LinkedList()
        self.assertEqual(None, lst.get_at_index(0))
    
    def test_get_at_index_multiple_elements_in_list(self):
        lst = LinkedList()
        lst.add_first(1)
        lst.add_first(2)
        lst.add_first(3)
        lst.add_first(4)

        self.assertEqual(4, lst.get_at_index(0))
        self.assertEqual(3, lst.get_at_index(1))
        self.assertEqual(2, lst.get_at_index(2))
        self.assertEqual(1, lst.get_at_index(3))

    def test_get_at_index_returns_none_when_index_out_of_bounds(self):
        lst = LinkedList()
        lst.add_first(1)
        lst.add_first(2)

        self.assertEqual(2, lst.get_at_index(0))
        self.assertEqual(1, lst.get_at_index(1))
        self.assertEqual(None, lst.get_at_index(2))
```

##### !end-tests

##### !hint

Create a `current` pointer that initially points to the `head` node to help you iterate through the list. You may also consider initializing an `index` variable that increments every time you look at a new node.

Still feeling stuck? Check this video walkthrough of the solution.
<!-- TODO: Add video walkthrough to explanation -->

##### !end-hint

##### !explanation
An example of a working implementation:

```py
    def get_at_index(self, index):
        current_index = 0
        current = self.head

        while current_index < index and current:
            current_index += 1
            current = current.next

        if current_index == index and current:
            return current.val
        return None

```
##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->



<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: e55ebc0e-ef57-4e2c-9878-96fff8b0f93c
* title: `get_at_index` Time Complexity
* points: 1

##### !question

What is the time complexity of `get_at_index`?

##### !end-question

##### !options

a| O(1)
b| O(log n)
c| O(n log n)
d| O(n)
e| O(n^2)

##### !end-options

##### !answer

d|

##### !end-answer


##### !explanation
The time complexity will be O(n) or linear as in the worst case, we will loop through every element in our linked list. 

##### !end-explanation

### !end-challenge
<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: a9f200c7-31cd-4ced-8edd-2915551b9562
* title: Space complexity `get_at_index`
* points: 1

##### !question

What is the space complexity of `get_at_index`?

##### !end-question

##### !options

a| O(1)
b| O(log n)
c| O(n log n)
d| O(n)
e| O(n^2)

##### !end-options

##### !answer

a|

##### !end-answer


##### !explanation
The space complexity will be O(1) or constant as we are not creating any new data structures or call stacks whose size are proportional to the length of our list.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: f8d82359-c9fe-4392-b478-15d534ef65b1
* title: `add_last`
* points: 1
  
##### !question

Implement a method `add_last` that inserts a new node with a given value as the new last node of the linked list.

##### !end-question

##### !placeholder
```py
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
    
    def add_first(self, value):
        new_node = Node(value)
        new_node.next = self.head
        self.head = new_node

    def add_last(self, value):
        #write your code here
        pass
```

##### !end-placeholder

##### !tests
```py
import unittest
from main import *

class LinkedListExtended(LinkedList):
    
    def get_first(self):
        if self.head:
            return self.head.value
        return None

    def get_at_index(self, index):
        current_index = 0
        current = self.head

        while current_index < index and current:
            current_index += 1
            current = current.next

        if current_index == index and current:
            return current.val
        return None
    
    def length(self):
        count = 0
        current = self.head
        while current:
            count += 1
            current = current.next
        return count

    def get_last(self):
        if not self.head:
            return None

        current = self.head
        while current.next:
            current = current.next
        return current.value
        

class TestPython1(unittest.TestCase):
    def test_add_last_on_empty_list(self):
        lst = LinkedListExtended()
        lst.add_last(1)
        self.assertEqual(1, lst.get_at_index(0))

    def test_add_last_on_empty_lst_head_is_tail(self):
        lst = LinkedListExtended()
        lst.add_last(1)
        self.assertEqual(1, lst.get_last())
        self.assertEqual(1, lst.get_first())
    
    def test_add_last_increases_length(self):
        lst = LinkedListExtended()
        
        self.assertEqual(0, lst.length())

        lst.add_last(5)

        self.assertEqual(1, lst.length())

        lst.add_last(4)
        self.assertEqual(2, lst.length())

        lst.add_last(3)
        self.assertEqual(3, lst.length())

    def test_add_last_adds_new_item_to_back_of_list(self):
        lst = LinkedListExtended()

        self.add_last(3)
        self.assertEqual(3, self.get_last())
        self.assertEqual(3, self.get_first())

        self.add_last(2)
        self.assertEqual(2, self.get_last())
        self.assertEqual(3, self.get_first())

        self.add_last(1)
        self.assertEqual(1, self.get_last())
        self.assertEqual(3, self.get_first())
```

##### !end-tests

##### !hint
Start by creating the new node with the `value` passed in.

The ultimate goal for this function is to redirect the current last node in the list to point at the new node last node in the list.

Consider how you might handle the edge case in which the list is empty. 

In the nominal case, where the list already has some number of nodes, consider using a `current` pointer to find the last node in the list. Recall that the last node in the list will have a `next` pointer with a `None` value. 


Still feeling stuck? Check this video walkthrough of the solution.
<!-- TODO: Add video walkthrough to explanation -->

##### !end-hint

##### !explanation
An example of a working implementation:

```py
    def add_last(self, value):
        if not self.head:
            self.add_first(value)
        else:
            new_node = Node(value)
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

```
##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 72c16689-c332-4922-bc1b-bf94ee82ce49
* title: `add_last` Time Complexity
* points: 1

##### !question

What is the time complexity of `add_last`?

##### !end-question

##### !options

a| O(1)
b| O(log n)
c| O(n log n)
d| O(n)
e| O(n^2)

##### !end-options

##### !answer

d|

##### !end-answer


##### !explanation
The time complexity will be O(n) or linear as in the worst case, we will loop through every element in our linked list. 

##### !end-explanation

### !end-challenge
<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: c9612963-f091-48cd-b928-d25ed10efa8f
* title: Space complexity `add_last`
* points: 1

##### !question

What is the space complexity of `add_last`?

##### !end-question

##### !options

a| O(1)
b| O(log n)
c| O(n log n)
d| O(n)
e| O(n^2)

##### !end-options

##### !answer

a|

##### !end-answer


##### !explanation
The space complexity will be O(1) or constant as we are not creating any new data structures or call stacks whose size are proportional to the length of our list.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### Removing a node at a specific index

To remove a node at a specific index, we also have to traverse the list until we find the index before the node to delete. Remove also requires some more complex redirection of pointers. If the node to remove is the head, then the head becomes the next element. In all other cases for a singly linked list, we adjust the prior node's `next` reference to point **past** the node you are removing.  

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

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 0cc4fc7c-9900-4e3c-9760-608114390a61
* title: Reverse a linked list
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (Checkpoints only, optional the topics for analyzing points) -->

##### !question

We can also tackle reversing a linked list by traversing the list and redirecting pointers as we go along. Write a method `reverse` to reverse the given linked list. The function should not return anything.

##### !end-question

##### !placeholder

```py
class Node:
    def __init__(self, value):
        self.val = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def reverse(self, value):
        #write your code here
        pass
```

##### !end-placeholder

##### !tests

[the unit tests below will run against the student submission]
```py
import unittest
from main import *

class LinkedListExtended(LinkedList):
    
    def add_first(self, value):
        new_node = Node(value)
        new_node.next = self.head
        self.head = new_node
    
    def get_first(self):
        if self.head:
            return self.head.value
        return None

    def get_at_index(self, index):
        current_index = 0
        current = self.head

        while current_index < index and current:
            current_index += 1
            current = current.next

        if current_index == index and current:
            return current.val
        return None


class TestPython1(unittest.TestCase):

    def test_reverse_empty_list(self):
        lst = LinkedListExtended()

        self.assertEqual(None, self.get_at_index(0))
    
    def test_reverse_will_reverse_five_element_list(self):
        lst = LinkedListExtended()
        for i in range(0, 5):
            lst.add_first(i)
        
        lst.reverse()

        for i in range(0,5):
            self.assertEqual(i, lst.get_at_index(i))
```

##### !end-tests

##### !hint
Initialize three pointers: `previous`, `current`, and `next`. `previous` and `next` should be initialized to `Null`, while `current` should start as the `head`.

Iterate through the list. 

At each iteration:
- Store `current`'s next, in `next`
- Redirect `current`'s next to point to the `previous` node. 
- Redirect both `previous` and `current` to point to their respective next nodes in the list

Still feeling stuck? Check this video walkthrough of the solution.
<!-- TODO: Add video walkthrough to explanation -->

##### !end-hint

##### !explanation
An example of a working implementation:

```py
    def reverse(self):
        if not self.head:
            return
        
        current = self.head
        previous = None
        
        while current:
            next = current.next
            current.next = previous
            previous = current
            current = next
        
        self.head = previous

```

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 21ecd57d-f336-471f-8548-f65a9e20ee3f
* title: Time Complexity of reverse
* points: 1

##### !question

What is the time complexity of `reverse`?

##### !end-question

##### !options

a| O(1)
b| O(log n)
c| O(n log n)
d| O(n)
e| O(n^2)

##### !end-options

##### !answer

d|

##### !end-answer


##### !explanation
The time complexity will be O(n) or linear as in the worst case, we will loop through every element in our linked list. 

##### !end-explanation

### !end-challenge
<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: 1c87985b-63f4-47cf-9335-8b44c5c16ffe
* title: Space complexity of reverse
* points: 1

##### !question

What is the space complexity of `reverse`?

##### !end-question

##### !options

a| O(1)
b| O(log n)
c| O(n log n)
d| O(n)
e| O(n^2)

##### !end-options

##### !answer

a|

##### !end-answer


##### !explanation
The space complexity will be O(1) or constant as we are not creating any new data structures or call stacks whose size are proportional to the length of our list.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->
