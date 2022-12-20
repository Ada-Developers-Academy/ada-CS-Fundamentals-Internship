
# Supplemental Concepts

## The Call Stack

As methods get called in an application, the system stores the current instruction addresses, local variables etc on a stack known as the _system call stack_.  Then when a method ends, the topmost method is popped off the stack allowing the system to resume execution.

![Memory Layout Diagram](images/memory-layout.png)

The diagram below shows the memory used by a running application.  At the top, the text in the application, and global variables are stored.  Below them is the dyanmic data allocated.  At the bottom the system stack stores the functions called.

```python
def function_a(x):
    y = 4
    z = function_b(x, y)
    print(f"The number is {z}")


def function_b(x, y):
  # pause application
    return x + y

x = 3
function_a(x)
```

For the code snippet above, the stack frame at the `# pause application` line would look like this:

![Stack frame example](images/call-stack.png)

<!-- Graphic saved at: https://drive.google.com/file/d/1SsxrrqIIw5oYonpKzwxvXAF3lTcQmB10/view?usp=sharing -->

- As the application starts the system puts the main part of the application on the stack, and then main calls `function_a`.  
- The system saves the arguments to `function_a` onto the stack, the address to return to (Main) when the method is finished and the local variabes in `function_a`.  
- `function_b` is called and the system saves the arguments to `function_b` onto the stack, the return address (`function_a`) and any local variables in `function_b`.  
- When `function_b` finishes, its stack frame is popped off the stack, and the return address is used to resume `function_a`.  
- When `function_a` finishes the same pop operation is performed and the application returns to main.  
- When the main part of the application is finished, its stack frame is popped off and the application terminates.  


When an error is raised, the stack is popped until the error is rescued in the current method, or the application terminates and a trace of all the elements on the stack at the time of the error is reported.


## Pointers & References

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

## Memory Leaks

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

## Resources

- [Current Slide Deck Used](https://docs.google.com/presentation/d/1lJ8WJnA6qRlHAIaRAjim3kiL4nRBWT5qvFGQQIB4EL4/edit?usp=sharing)
- [Past Slide Deck Used In Class](https://drive.google.com/file/d/0B__DV26QHsH4bFczWXBXdGtHYkE/view?usp=sharing)
- [Linked Lists from Geeks for Geeks](https://www.geeksforgeeks.org/data-structures/linked-list/) - Lots of articles & practice problems
- [Stanford LinkedList Basics](http://cslibrary.stanford.edu/103/LinkedListBasics.pdf)
