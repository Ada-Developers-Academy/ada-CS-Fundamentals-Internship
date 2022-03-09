# Activity:  Problem Solving

## Goal

Our goal is to practice manipulating list nodes.

## Review Linked List Lesson

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: checkbox
* id: 0b2ff1c9-8ec8-4431-a9ef-8855a7841c43
* title: Where are Linked Lists Optimal
* points: 1
* topics: linked-lists, big-o

##### !question

In which scenarios are linked lists more time efficient than arrays?

##### !end-question

##### !options

* Inserting to the front of the list
* Inserting to the rear of the list
* Inserting to the middle of the list
* Removing from the front of the list
* Removing from the rear of the list
* Removing from the middle of the list
* Finding an element by it's index

##### !end-options

##### !answer

* Inserting to the front of the list
* Removing from the front of the list

##### !end-answer

##### !hint

Remember to find an element by it's index in a linked list requires traversing the list. Also, removing an element from the front of an array requires shifting all elements to the left.

##### !end-hint

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: a701574a-1eea-401a-b2d6-e59ab58b1c47
* title: What type of Linked List is illustrated below?
* points: 1
* topics: python, linked-lists

##### !question

What type of data structure is the following linked list?

![Linked List Example Drawing](./images/linkedlist.svg)

##### !end-question

##### !options

* Singly Linked List
* Doubly Linked List
* Circular Linked List

##### !end-options

##### !answer

* Doubly Linked List

##### !end-answer

##### !explanation

A doubly linked list is a linked list in which each node has a pointer to the previous node as well as the next node.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: ab2f5a80-f005-43f1-8dbd-64c14a57380b
* title: What is an advantage of using a doubly linked list?
* points: 1
* topics: python, linked-lists, doubly-linked-lists

##### !question

Why use a doubly linked list over a singly linked list?

Are there any advantages to having a `tail` reference as well as the `head`?

##### !end-question

##### !placeholder

Why use a doubly linked list?

##### !end-placeholder

##### !explanation

A doubly linked list enables traversing the list in both directions and combined with a `tail` reference makes adding and removing nodes from the end of the list more efficient, `O(1)` instead of `O(n)`.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: paragraph
* id: 25d94120-fa67-472e-ae1f-3586ca79bf25
* title: Explain in your own words

##### !question

In your own words, why are Linked Lists useful?

##### !end-question

##### !placeholder

Why linked lists?

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Livecode

### Project Introduction

As a class we will check out  the [project](./03-linked-list-checkpoint.md) and work through a couple of the methods.  The purpose is to gain familiarity with the project and to learn how to write Linked List code.

### Sample Interview Problem Livecode

- [Activity Replit](https://replit.com/@adadev/linked-list-practice#README.md)

## Activity - Group Work Linked List Methods

After the class livecode working on rotating a linked list, we will break into groups to work on the Palindrome Linked List method.

### Getting Started

In small groups of 3-4, **one student** will *fork* the given replit and then share a collaboration link with the rest of the team.

### Exercise

As a team complete the pair of methods in the linked replit.

If you finish early, you can depart the session or work on the project, with instructor support available.