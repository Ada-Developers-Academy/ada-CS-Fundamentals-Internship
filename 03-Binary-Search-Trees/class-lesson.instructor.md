# Lesson Plan

Binary Search Trees and trees in general are a core learning concept in computer science and a common interview question. This unit compromises focusing on BSTs in particular and just introduces trees in general. This is to support interviewing and give students a start with more advanced data structures.

In prior years more general tree information was presented, but it was knowledge-level material that was not relevant to interviews and was difficult to retain.  So this unit focuses on hands-on work with BSTs.

Also the project does not involve removing an element from a tree.  It was removed to improve the submission rate on the project as this is the 1st really hard project. Instead that's the livecode.

## Lesson Goals

We want students to:

- Get comfortable with TreeNodes
  - Write code to add, and find nodes to a tree
  - Manipulating them to add and find nodes in a tree
  - Conduct traversals on a tree
  - Write recursive code
  - Identify the time complexity of methods involving BSTs

## Review Linked Lists Project - 10 minutes

Start off the lesson by welcoming students to the class and note attendance. You can use the Airtable to record attendance The [C16 Airtable](https://airtable.com/appkfPQ769uxQLSei/tbl6oiA8ZG1wKUonM/viwgf4wesbLFMlg1L?blocks=hide) is linked.

Take a moment to review any questions from Linked Lists and allow students to present their solutions.

### !callout-info

## Students may not want to do this

Students can be a bit shy, but you can contact specific students ahead of time asking them to be ready to present, "because you find their solution interesting."  Being prepared helps with student confidence.

### !end-callout

## BST Review

Do a problem set review for any challenge questions posed in [Ordered Collections of Data](./01-Ordered-Collections-Of-Data.md), [BST Implementation](./02-Binary-Search-Trees.md), [Balancing](./03-Binary-Search-Trees-Height-Big-O.md), and [Serialization](./04-Binary-Search-Trees-Traversal.md)

Focus on space complexity of recursive implementations vs iterative solutions, strategies for implementing recursive solutions and why recursion can still be useful given the bigger space complexity, and DFS/BFS. 

Part of the goal of this lesson is to set them up to understand graphing algorithms, particularly DFS and BFS. 
git restore
Specifically reinforce:

- BSTs are great when order needs to be maintained with good insertion, deletion, and lookup times.

## Livecode - 20 minutes

In the livecode walk through breadth first search.

Remember to:

- Try to get students to navigate as you type.  
- Cause a bug, and try to promote student ideas to fix it.
- Model how to use the tests and print statements.

## Coding Activity - 40 minutes

Break students into breakout rooms to practice depth first search traversals. Optionally you can talk through some pseudocode before students start working.

Iterate through the breakout rooms answering questions as you go.

## Solution Examples

Solutions:
- [Solution to DFS activity is in the `solution` branch](https://github.com/Ada-Activities/bst-dfs-practice)