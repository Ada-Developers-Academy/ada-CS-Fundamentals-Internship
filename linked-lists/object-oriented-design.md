# Object Oriented Design

## Encapsulation

When designing a data structure like a Linked List, we typically design the data structure as abstract, hiding implementation.  So the designer could switch a LinkedList into an ArrayList without impacting user functionality.  They could also transition into a DoublyLinkedList without impacting users.  

## Node Class

The node class encapsulates each element of the LinkedList..  It provides an attribute to store data and a node referencing the next node in the chain.  It provides an interface for our LinkedList to deal with the data and connect nodes.

```python
# Defines a node in the singly linked list
class Node:
    def __init__(self, value):
        self.data = value
        self.next = None
```

![Linked List Node](images/nodeLinkedList.png)

## Linked List Class

### constructor

### `get_first`

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

### `add_first`: Adding A Node at the Head

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

### `add_last` (code challenge)