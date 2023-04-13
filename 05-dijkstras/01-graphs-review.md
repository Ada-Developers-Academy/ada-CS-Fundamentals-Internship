# Graphs Review

## Overview of Graphs
In the previous topic, we talked about graphs, how to represent them, and two algorithms - breadth first search and depth first search - for traversing graphs. In this topic, we'll review and extend some key concepts from the previous topic. We'll also introduce Dijkstra's algorithm which will allow us to solve a new subset of graph problems. 
<!-- Add more advanced review questions -->


<!-- ======================= END CHALLENGE ======================= -->

## Review of Breadth First Search & Depth First Search

### Breadth First Search (BFS)
Recall from the last lesson that the breadth first search (BFS) algorithm starts its traversal with a particular node and then visits each node connected to the starting node before expanding outward.

![Breadth First Search on an Undirected Graph](images/bfs-undirected-graph.gif)

BFS uses a queue to visit nodes in order of proximity to the starting node. It accomplishes this by first adding each of the neighbors of the starting node to the queue. The algorithm then removes nodes from the queue one at a time, adding any unvisited neighbors of each node it removes to both the queue for further processing and the list of visited nodes.

### Depth First Search (DFS)
You may also recall from the last lesson that the Depth First Search (DFS) algorithm starts at a node and then follows a path as deeply as possible before backing up and following the next path. We refer to this traversal pattern as back-tracking.

The DFS algorithm requires the use of a stack. The stack is used to further process nodes along the path, starting with the first node and then adding its neighbors to the stack before iterating on the nodes added to the stack.

#### DFS Visualization
<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=757ce80b-3cc5-4ae0-bdf1-af240146d5a0&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

<!-- Add question -->

### Using Breadth First Search to Find the Shortest Path in an Unweighted Graph

Breadth first search can easily be adapted to find the shortest path between any two nodes in an unweighted graph. In order to retrieve the shortest path using the BFS algorithm, we would need to modify the algorithm to store the current shortest distance to the target node as well as the preceding node in the shortest path. This is essentially what Dijkstra's algorithm does, which we will learn more about in the next section. 

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
