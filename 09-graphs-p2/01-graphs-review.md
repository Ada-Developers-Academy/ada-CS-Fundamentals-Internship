## Overview of Graphs
In the previous lesson, we talked about graphs, how to represent them, and a couple algorithms for traversing graphs. In this lesson, we'll go over a quick review of some of the learnings from the last lesson and introduce a new algorithm that can be used to solve a multitude of graph problems.

## Graph Representation Review Questions

You may recall in the previous lesson that graphs are a linked abstract data structure in computer science represented by a set of *nodes* connected by what are called *edges*. 

Let's review how to represent a graph via a list of edges, an adjacency matrix, and an adjacency dictionary.

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: 3490f39e-c8e4-4eaa-9908-ba5407937934
* title: Representing a Graph with a List of Edges
* points: 0

##### !question

Which list of edges represents the graph shown in the diagram below? Assume the graph is undirected.

![Graph representing list of edges](images/graph_2.png)

##### !end-question

##### !options

a| ```py
[
    [0, 2],
    [1, 3],
    [2, 3]
]
```
b| ```py
[
    [0, 3],
    [0, 1],
    [1, 4]
]
```
c| ```py
[
    [0, 3],
    [0, 1],
    [1, 4],
    [1, 3]
]
```
d| ```py
[
    [0, 3],
    [0, 1],
    [1, 2],
    [1, 4]
]
```

##### !end-options

##### !answer

d|

##### !end-answer

### !explanation
Answer D is the correct answer because all of the edges in the graph are represented and correspond correctly to the edges in the graph.

[0, 3] indicates the edge from node 0 to node 3.
[0, 1] indicates the edge from node 0 to node 1.
[1, 2] indicates the edge from node 1 to node 2.
[1, 4] indicates the edge from node 1 to node 4.

### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: bc42d1a0-b66a-4cc2-ad42-b2b5c51323c1
* title: Representing a graph with an adjacency matrix
* points: 0

##### !question

Which adjacency matrix represents the graph shown in the diagram below? Assume the graph is undirected.

![Graph representing adjacency matrix](images/graph_1.png)

Assume the letters are mapped to the following indices:
* A -> 0
* B -> 1
* C -> 2
* D -> 3
* F -> 4
* Z -> 5

#### Option A
![Adjacency Matrix A](images/adj_matrix_2.png)

#### Option B
![Adjacency Matrix B](images/adj_matrix_1.png)

#### Option C
![Adjacency Matrix C](images/adj_matrix_3.png)

##### !end-question

##### !options

a| Option A
b| Option B
c| Option C

##### !end-options

##### !answer

b|

##### !end-answer

##### !explanation

Option B is the correct answer because the edges in the graph are all represented in the adjacency matrix.

For instance:

Row A, column C (Matrix[A][C]) is true because there exists an edge between node A and node C. Similarly, row C, column A (Matrix[C][A]) is true because of the same edge. 

Each cell containing true denotes an edge between the corresponding nodes.

Row Z is all false because node Z does not share an edge with any other node.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 2a316cff-6a03-4d90-9d15-4cf299afd223
* title: Representing a graph with an adjacency dictionary
* points: 0

##### !question

Which graph is represented by the following adjacency dictionary?

```py
adjacency_dict = {
    "Seattle": ["Portland"],
    "Portland": ["Dallas", "Seattle"],
    "Detroit": ["Dallas"],
    "Dallas": ["Boston", "Detroit", "Portland"],
    "Boston": ["Dallas"]
}
```

#### Option A
![Graph A](images/graph_a.png)

#### Option B
![Graph B](images/graph_b.png)

#### Option C
![Graph C](images/graph_c.png)

##### !end-question

##### !options

a| Option A
b| Option B
c| Option C

##### !end-options

##### !answer

a|

##### !end-answer

##### !explanation

Option A is correct because the nodes/edges in the adjacency dictionary correspond with the nodes and edges in the graph. 

For instance:

* Seattle is connected to only one city: Portland
* Portland is connected to Dallas and Seattle
* Dallas is connected to Boston, Detroit, and Portland
* Detroit is connected to Dallas
* Boston is connected to Dallas

##### !end-explanation 

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Review of Breadth First Search & Depth First Search

### Breadth First Search (BFS)
You may recall from the last lesson that the Breadth First Search (BFS) algorithm starts with a particular node and then visits each node connected to the starting point before expanding outward.

The BFS algorithm requires us to use a queue to visit nodes in a "level-by-level" ordering by adding each of the neighbors of the starting node to the queue. We then loop through the queue, adding unvisited neighbors to the list of visited nodes as well as to the queue to be further processed.

#### BFS Visualization
<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=370ea67c-477d-41c7-b066-af240146d5c9&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

### Depth First Search (DFS)
You may also recall from the last lesson that the Depth First Search (DFS) algorithm starts at a node and then follows a path as deeply as possible before backing up and following the next path. We refer to this algorithm as a back-tracking algorithm.

The DFS algorithm requires the use of a stack. The stack is used to further process nodes along the path, starting with the first node and then adding its neighbors to the stack before iterating on the nodes added to the stack.

#### DFS Visualization
<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=757ce80b-3cc5-4ae0-bdf1-af240146d5a0&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

### Why BFS (kinda) allows for shortest path of an unweighted graph

By itself, BFS as we developed it does *not* allow for finding the shortest path of an unweighted graph. In order to retrieve the shortest path using the BFS algorithm, we would need to modify the algorithm to store the current shortest distance to the target node as well as the preceding node in the shortest path. This is essentially what Dijkstra's algorithm does, which we will learn more about in the next section. 

Again, you may recall BFS visits nodes based on *proximity*. It starts by visiting nodes one edge away from the start node (its neighbors). Then it visits nodes that are two edges away from the starting node (neighbor's neighbors), etc. Therefore, the BFS algorithm can be modified to record the smallest path from an initial node to any other connected node in the graph. The big difference between Dijkstra's Algorithm and BFS is that Dijkstra's uses the *weights* of the edges to determine the next node to consider rather than just the number of edges. Again, we'll talk about Dijkstra's algorithm more in the next section.

### Why DFS does not find shortest path

The main reason the DFS algorithm is not typically used to find the shortest path is because DFS is not a "greedy" algorithm. The algorithm is not designed to account for changes in logic based on the data it encounters, which is what is needed for finding the shortest path in a graph.

The DFS algorithm does not take a nodes' proximity into consideration when making its traversal, so it's not useful for tracking the distance between nodes.

## !callout
A greedy algorithm is an approach for solving a problem by selecting the best option available at the moment. A greedy algorithm never reverses the earlier decision even if the choise is wrong. An algorithm which is considered greedy may not produce the best result for all problems.
## !end-callout

## BFS, DFS, or Either

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: e012797e-0060-4484-b3b4-245fa4152228
* title: BFS, DFS, Either, or Neither?
* points: 0

##### !question

If we are looking for a node in a graph that is many levels deeper than the starting node, is BFS, DFS, Either, or Neither the best option?

##### !end-question

##### !options

a| Breadth First Search
b| Depth First Search
c| Either
d| Neither

##### !end-options

##### !answer

b|

##### !end-answer

##### !explanation

The correct answer is B because it is faster and more efficent to reach nodes deeper in the graph with Depth First Search.

##### !end-explanation 

### !end-challenge

### !challenge

* type: multiple-choice
* id: b8569433-61d6-48e0-afa2-5b28e3e9facf
* title: BFS, DFS, Either, or Neither?
* points: 0

##### !question

If we are looking to find all the connected nodes in a graph, is BFS, DFS, Either, or Neither the best option?

##### !end-question

##### !options

a| Breadth First Search
b| Depth First Search
c| Either
d| Neither

##### !end-options

##### !answer

c|

##### !end-answer

##### !explanation

The correct answer is C because either algorithm can be used to find all of the connected nodes in a graph. They both have similar time complexity with DFS being only slightly faster on average.

##### !end-explanation 

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

## Introduction to Dijkstra's Algorithm

As mentioned earlier, a modified version of BFS only allows us to find the shortest path between two nodes in an unweighted graph. One way to further modify the BFS algorithm to find the shortest distance between two nodes is by implementing what is called Dijkstra's Algorithm. 

We will learn more about Dijkstra's Algorithm in the following lesson.
