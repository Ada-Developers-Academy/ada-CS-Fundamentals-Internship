# Instructor Notes

Linked Lists are a core learning concept in computer science and a common interview question. 

## Lesson Goals

We want students to:

- Get comfortable using ListNodes
  - Using them to traverse a list
  - Manipulating them to add and remove nodes
  - Identify the time complexity of methods involving linked lists

## Lesson Introduction - 10 minutes

Start off the lesson by welcoming students to the class and note attendance. You can use the Airtable to record attendance The [C16 Airtable](https://airtable.com/appkfPQ769uxQLSei/tbl6oiA8ZG1wKUonM/viwgf4wesbLFMlg1L?blocks=hide) is linked.

Then follow the 1st part of the [activity](./05-linked-list-activity.md) reviewing where linked lists are useful (when you need to add/remove to the front/rear of a list).  

## Livecode - 20 minutes

In the livecode walk through:

1.  Merge Sorted Lists from the text lesson
1.  Setup the project and write 2 methods

Remember to:

- Try to get students to navigate as you type.  
- Cause a bug, and try to promote student ideas to fix it.  
- Model how to use the tests and print statements.

## Coding Activity - 60 minutes

Break students into breakout rooms to practice the replit. Optionally you can complete one exercise as a class before breaking the remainder into groups.

Iterate through the breakout rooms answering questions as you go.

## Solution Examples

You can find a solution in [Chris' Replit](https://replit.com/@ChrisMcAnally/List-Practice-Solution#).

*Code Snippet: Merge Sorted Lists*
```py
from typing import Optional

class ListNode:
    def __init__(self, value, next = None):
        self.value = value
        self.next = next
    def __repr__(self):
        return f"ListNode({self.value})"

def transform_to_doubly_linked_list(head: ListNode):
    previous = None
    current = head
    while current is not None:
        current.previous = previous
        previous = current
        current = current.next

    return previous

def is_palindrome(head: Optional[ListNode]) -> bool:
    if head is None:
        return True

    tail = transform_to_doubly_linked_list(head)

    while (head != tail):
        if head.value != tail.value:
            return False
        head = head.next
        tail = tail.previous
    
    return True
```

*Code Snippet: Rotate Linked List*

```py

class ListNode:
    def __init__(self, value, next = None):
        self.value = value
        self.next = next

def add_first(head: ListNode, node: ListNode):
    node.next = head
    return node

def find_last_and_second_to_last(head: ListNode) -> ListNode:
    previous = None
    current = head

    while current.next is not None:
        previous = current
        current = current.next
    
    return (previous, current)

def rotate_list(head: ListNode, k: int) -> ListNode:
    
    if head is None:
        return None
    if k < 0:
        raise ValueError("k must be positive")
    elif k == 0 or head.next is None:
        return head
    
    for i in range(k):
        (new_tail, tail) = find_last_and_second_to_last(head)

        new_tail.next = None
        head = add_first(head, tail)

    return head
```

### !callout-secondary

## This isn't efficient

This is **not** an efficient solution.  To do this more efficiently (not O(nk) time), we would potentially need to transform this into a doubly linked list or copy it into an array, or calculate the length of the list and a way to rotate in reverse to get a similar outcome.

### !end-callout

