# Lesson Plan

Hash tables are a weird unit in that we don't expect students to *construct* a hash table, but instead to be able to use one. However students *do* need know understand the basic principles of how hash tables/dictionaries work.

## Lesson Goals

We want students to be able to:

- Explain Hash Table concepts such as:
  - Hash Function
  - Collisions
  - Common collision resolution methods
- Solve coding problems using Hash Tables

## Review Linked Lists Project - 10 minutes

Start off the lesson by welcoming students to the class and note attendance. You can use the Airtable to record attendance The [C16 Airtable](https://airtable.com/appkfPQ769uxQLSei/tbl6oiA8ZG1wKUonM/viwgf4wesbLFMlg1L?blocks=hide) is linked.

Take a moment to review any questions from Stacks & Queues and allow students to present their solutions.

### !callout-info

## Students may not want to do this

Students can be a bit shy, but you can contact specific students ahead of time asking them to be ready to present, "because you find their solution interesting."  Being prepared helps with student confidence.

### !end-callout

## BST Introduction - 10 minutes

Then follow the 1st part of the [activity](./03-hash-tables-activity.md) reviewing:

- Hash Table Concepts:
  - Hash Function
  - Collisions
  - Collision resolution methods
- Where Hash Tables really shine providing O(1) lookup times and where keys must be unique

Specifically reinforce:

- Hash tables can reduce iteration to look up items in Lists.
- Keys must be unique
- Hash tables are an example of a heuristic data structure which functions well _most_ of the time, but not always.

## Livecode - 20 minutes

In the livecode section review the project, but do not solve it for them, as this project is relatively brief.

Then work through the given coding problem on Replit making sure students lead the navigation and understand how it works.  Provide specific examples and use the replit's built-in examples to work through the problem.

- [Solution to 4Sum](https://replit.com/@adadev/4Sum-II-Solution)

### !callout-info

## DefaultDict

This is also a good chance to introduce `defaultdict` as an alternative to `dict`.

### !end-callout

## Coding Activity - 60 minutes

Break students into breakout rooms to practice the replit. Optionally you can talk through some pseudocode before students start working.

Iterate through the breakout rooms answering questions as you go.

## Solution Examples

Solutions:

- [The project](https://github.com/AdaGold/hash-practice/tree/python-solution)
- [4Sum](https://replit.com/@adadev/4Sum-II-Solution)
- [Inflight Entertainment](https://replit.com/@adadev/Inflight-Entertainment-solution)
- [Longest Palindrome](https://replit.com/@adadev/Longest-Palindrome-Solution)