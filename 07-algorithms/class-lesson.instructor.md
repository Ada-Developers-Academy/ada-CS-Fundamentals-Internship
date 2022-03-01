# Lesson Plan

Stacks and Queues are fairly straightforward data structures, but are included in the curriculum for completeness as they are a fundamental part of most computer science curriculums and often used in interviews.

They are expanded on in the project using a circular buffer. Students often find using the `%` operator to traverse an array in a circular buffer. Demonstrating it's use in a loop can be quite helpful.

## Lesson Goals

We want students to:

- Be able to explain Stacks & Queues
- Be able to explain Abstract Data Types
- Use Stacks & Queues to solve coding problems
- Use the modulus operator to traverse a circular buffer

## Review Binary Search Tree Project - 10 minutes

Start off the lesson by welcoming students to the class and note attendance. You can use the Airtable to record attendance The [C16 Airtable](https://airtable.com/appkfPQ769uxQLSei/tbl6oiA8ZG1wKUonM/viwgf4wesbLFMlg1L?blocks=hide) is linked.

Take a moment to review any questions from Binary Search Trees and allow students to present their solutions.

### !callout-info

## Students may not want to do this

Students can be a bit shy, but you can contact specific students ahead of time asking them to be ready to present, "because you find their solution interesting."  Being prepared helps with student confidence.

### !end-callout

## Stacks & Queues Introduction - 10 minutes

Then follow the 1st part of the [activity](./01-stacks-and-queues.md) reviewing stacks & queues, abstract data types & the use of the modulus operator when traversing a list.  

Specifically reinforce:

- The utility of Abstract Data Types
- The core stack & queue functions
- The use of the `%` operator to traverse a circular buffer
    - Students have trouble understanding how to wrap around a list without using an `if` statement.  Instead of using `front = (front + 1) % size`, they will use an if statement.  It's not a huge deal, but can be helpful to simplify code.

## Livecodes - 20 minutes

In the livecode walk through a sample stack coding problem and the constructor/`enqueue` method:

Remember to:

- Try to get students to navigate as you type.  
- Cause a bug, and try to promote student ideas to fix it.
- Model how to use the tests and print statements.

### Reorder Linked List Problem - 15 minutes

After introducing the project and illustrating the `%` in the `enqueue` method, we can walk through a sample problem using a Stack and give students another chance for exposure to Linked Lists.

- [Reordering a Linked List](https://replit.com/@adadev/reorderlinkedlist#reorder_linked_list/reorder_linked_list.py)

## Coding Activity - 45 minutes

Break students into breakout rooms to practice the replit. The replit has a suggested solution in pseudocode which is a good chance for students to discuss how to convert it to code.

Iterate through the breakout rooms answering questions as you go.

[Daily Temperatures](https://replit.com/@adadev/Daily-Temperatures-Solution#daily_temperatures/daily_temperatures.py)

## Solution Examples

Solutions:

- [The project](https://github.com/adagold/stacks-queues/tree/python-solution)
- [Reorder Linked Lists](https://replit.com/@adadev/reorderlinkedlist-Solution)
- [Daily Temperatures](https://replit.com/@adadev/Daily-Temperatures-Solution)
