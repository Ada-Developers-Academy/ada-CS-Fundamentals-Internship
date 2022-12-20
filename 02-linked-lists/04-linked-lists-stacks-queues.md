# Applications of Linked Lists

## Overview

Linked lists have a variety of practical applications. Imagine a playlist in your favorite music application. Each song in the playlist represents a node in a doubly linked list. We can add new songs onto the end of our playlist in O(1) time. As we listen to our playlist, it is very easy to replay or skip a song using our previous and next pointers. 

We might also imagine the undo and redo functions of a word processor or other software. Each change to our word document is stored in a node in a doubly linked list. We can undo and redo our changes by traversing our list backwards and forwards.

Linked lists are also prove useful when implementing many other data types that fall into a category called _abstract data types_.

## Abstract Data Types

An _Abstract Data Type_ (ADT), is a type of object which is described by the methods it has and how they perform. Implementation details are not included.  You could for example create a `List` class. You can provide methods to add elements and retrieve elements at a given index. The user of your class never needs to know if you used an array or linked list to store the information internally. The class is called _abstract_ because the data structure's description is independent from it's implementation.  

Linked lists are not considered abstract data types, because a key feature of a linked list is that is implemented by linking nodes together in a chain. However, as mentioned previously, linked lists are often used to implement abstract data types.

Two abstract data types often implemented with linked lists are stacks and queues. Stacks and queues are, like linked lists, ordered linear collections of data. Unlike linked lists, they are described by what they do, rather than how they are implemented. This means that while we might choose to implement stacks and queues with a linked list, we could also choose to implement them with an array.

## Stacks

A stack is a data structure which stores a list of data and only provides access in a Last-In-First-Out (LIFO) order. You've seen stacks before at Ada. When we discussed recursion we noted that function calls are saved on the system stack. This is so the most recent function called is the first function returned to when the current function ends.

A stack provides the following methods:

- **push(item)** - This method puts an item into the stack at the top.
- **pop** - This method removes and returns the item on the top of the stack.
- **is_empty** - This method returns true if the stack is empty and false otherwise.

A stack might also implement a `peek` method which returns, but does not remove the item on top of the stack, and a `size` method which returns the number of items currently on the stack.

We can picture a stack like a stack of plates where new plates can be added and removed from the top, but cannot be removed from the middle or bottom of the structure.

![Stack Diagram](images/stack.png)

### Implementation of a Stack

We can use any linear data structure to implement a stack.  For example, using a linked list, we could implement a `Stack` class like this:

```python
class Stack:
  
    def __init__(self):
        self.store = LinkedList()

    def push(self, item):
        self.store.add_first(item)

    def pop(self):
      return self.store.remove_first()

    def empty(self):
        return self.store.length() == 0
```
Linked lists are a popular choice for stack implementations because insertion and deletion, or `push` and `pop` in the case of our stack, are O(1) operations with linked lists. However, because a stack is an ADT, our `Stack` class doesn't _have_ to be implemented with a linked list. We could later change the implementation to use an array, and the users of the class would not need to change any of their code. This is because the implementation is _hidden_ behind a public interface. The top of the stack would reference the last element in the array. 

**Stack ADT**
![Stack ADT](images/stackADT.png)

The implementation code in the diagram above could make use of any data structure - a linked list, array, or something else - so long as it implements the method to its specification.


## Queues

A queue unlike a stack operates in a First-In-First-Out (FIFO) order.  Like a line of people at a concert, the first element to enter the queue is the first element removed.  

![Queue Diagram](images/queue.png)

As shown above elements are added to the back of the queue in an operation called _enqueue_ and removed with an operation called _dequeue_.  

Queues are great for any operation that needs to work with data in a first-in-first-out order.  For example some systems have worker processes which can be assigned tasks to work on and these worker processes take on jobs assigned to them in the order they appeared, completing one before taking on the next.

A Queue provides the following methods:

- **enqueue(item)** - This method puts an item into the back of the queue.
- **dequeue** - This method removes and returns the item at the front of the queue.
- **is_empty** - This method returns true if the queue is empty and false otherwise.

### Queue Implementation Considerations

Like a stack, a queue can be implemented several ways and the implementation should be hidden from the user. One way would be to implement a queue with a linked list like this:

```python
class Queue:
    def __init__(self):
        self.store = LinkedList.new

    def enqueue(self, item):
        self.store.add_last(item)

    def dequeue(self):
        if self.is_empty():
            return None

        self.store.remove_first()

    def is_empty(self):
        return self.store.empty()
```

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: bade61da-8d68-401f-abd1-345fbd38bc4b
* title: Enqueue & Dequeue
* points: 1
* topics: queues, linked lists

##### !question

What would be the Big-O of enqueue and dequeue for the above queue implementation?

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n log n)
* O(n^2)
* It depends

##### !end-options

##### !answer

* It depends

##### !end-answer

<!-- other optional sections -->
##### !hint

Do all LinkedList implementation have the same time complexity for add_last and remove_first? Do we know the internal implementation of the LinkedList class?

##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

If the Linked List has a tail reference and is a doubly linked list, then both enqueue and dequeue can be done in O(1) time.  If there is no tail reference then enqueue should perform in O(n) time.

##### !end-explanation

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: 44b75a3a-ebb1-4b05-ba0e-39ecf8675e7e
* title: Why might we prefer to implement a queue with a linked list instead of an array?
* points: 1

##### !question

Why might we prefer to implement a queue with a linked list instead of an array?

##### !end-question

##### !placeholder



##### !end-placeholder
<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation
With a doubly linked list that maintains a tail pointer, we can enqueue and dequeue elements from the queue in O(1) time. With an array, recall that inserting or removing an element of an array can be expensive as all items after the item inserted or removed need to be shifted over by 1. 

##### !end-explanation 

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->
<!-- ======================= END CHALLENGE ======================= -->



