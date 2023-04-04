## Graph Algorithms

There are a huge [class of algorithms](https://en.wikipedia.org/wiki/Category:Graph_algorithms) involving graphs.  We will look at two of the most common graph algorithms as a sample.  

### Breadth First Search

Like in a binary search tree a breadth first search (BFS) in a graph is performed with a queue.  However, unlike trees, graphs often have cycles so we will need to keep track of the nodes we have visited and ensure that we only traverse nodes that have yet to be visited. Otherwise, we will get stuck in a loop visiting the same nodes in the cycle over and over again.

### !callout-info

## Cycles in Graphs
In graph theory, a path that starts from a given node and ends at that same node is called a *cycle*. In the graph below, there is a cycle starting from node A -> node B -> node C -> node A.

![graph with cycle](images/directed-graph.png)

### !end-callout

In breadth first search (BFS)we start with a particular node and visit each node connected to the starting point in the graph starting with the closest node to the starting point and expanding outward.

We do so by adding each of the neighbors of the starting node to a queue. Then we loop through the queue, removing the first element in the queue and adding each of its unvisited neighbors to the queue. We repeat this process until the queue is empty. 

Once the queue is empty we know we have visited all nodes in the graph that are possible to reach from the starting node.

![Breadth First Search](images/bfs.gif)

In the above visualization, the algorithm starts its traversal from the specified start node, node 0 in this case, and expands outwards. First the algorithm visits the start node's neighbors, then the neighbor's neighbors, and so on until it has traversed every node reachable from the start node. If a neighbor has already been visited, the algorithm skips over visiting that neighbor and moves on to the next unvisited neighbor.

You can also interact with a breadth first search animation on [HackerEarth](https://www.hackerearth.com/practice/algorithms/graphs/breadth-first-search/visualize/)

**Breadth First Search Pseudocode Walkthrough**
<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=493ecb29-6431-4e61-b918-af170141a8da&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="360" width="640" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

The pseudocode for breadth first search is as follows:
```
    - Initialize an empty list of visited nodes
    - Initialize an empty queue 
    - Add the node we would like to start our traversal from to the queue 
    - Add the node we would like to start our traversal from to visited
    - While the queue is not empty:
        - Remove an element from the queue and store it in a variable, `current`
        - Loop through each of the current node's neighbors:
            - If the neighbor has not yet been visited:
                - Add the neighbor to the queue
                - Add the neighbor to the list of visited nodes
    - Return the list of visited nodes
```
Notice that because the breadth first search algorithm asks us to loop through each node's neighbors, it is most convenient when the graph being traversed is represented as an adjacency list or dictionary. If graph `g` is represented as an adjacency list, we can easily access a list of node `n`'s neighbors with `g[n]`. Looping through `n`'s neighbor's would simply mean looping through each element in `g[n]`.  

![Accessing a Node's Neighbors with an Adjacency List](images/graph_neighbors_adj_list.png)

If the graph is provided to us as an adjacency matrix, it is still possible to loop through the graph's neighbors. However, when `g` is changed to an adjacency matrix, note that `g[n]` is now a list of _all the nodes in the graph_ - not just node `n`'s neighbors - with `g[n][i]` indicating whether there is an edge from node `n` to node `i`. To loop through node `n`'s neighbors, we have to check the value of `g[n][i]` for all `i` in `g[n]` to determine whether `n` and `i` are neighbors. 

![Accessing a Node's Neighbors with an Adjacency Matrix](images/graph_neighbors_adj_list.png)

If the graph is represented by a list of edges it is difficult to find a node's neighbors because we need to search the entire list of edges for edges from node `n`. For this reason, when we are interested in performing breadth first search on a list of edges, it is common to convert the list of edges to an adjacency list or adjacency matrix. 

![Accessing a Node's Neighbors with a List of Edges](images/graph_neighbors_list_of_edges.png)

Some implementations of a breadth first search may have the user pass in the node they would like the traversal to start at as a parameter. Other times, breadth first search implementations will start their traversal with a random node in the graph or the first node listed in the given graph representation.

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 911d76a6-f2c5-4f94-97b9-c1d5477c0502
* title: Breadth First Search on a Disconnected Graph
* points: 1

##### !question

Using the pseudocode included in the above lesson, if we begin our traversal from `Seattle`, what will a Breadth First Search return as its list of `visited` nodes for the following graph?

```python
    g = {
        "Seattle": ["Portland", "Chicago"],
        "Chicago": ["Seattle"],
        "Portland": ["Seattle", "Kona"],
        "Kona": ["Portland"],
        "Miami": ["El Paso"],
        "El Paso": ["Miami"]
    }
```
![Disconnected Graph](images/disconnected-graph-example.png)

##### !end-question

##### !options

a| `visited = ["Seattle", "Portland", "Chicago", "Kona"]`
b| `visited = ["Seattle", "Chicago", "Portland", "Kona"]`
c| `visited = ["Seattle", "Portland", "Chicago", "Kona", "El Paso", "Miami"]`
d| `visited = ["Seattle", "Portland", "Chicago", "Kona", "Miami", "El Paso"]`

##### !end-options

##### !answer

a|

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

Seattle will be added to visited first because Seattle is our specified start node. So visited is `["Seattle"]`.

<br>

We loop through Seattle's neighbors. Since the graph is provided as an adjacency dictionary, we will loop through Seattle's neighbors in the order they are listed in the adjacency dictionary. `g["Seattle"]` is `["Portland", "Chicago"]` so we will visit Portland first, then Chicago. Our visited list is now `["Seattle", "Portland", "Chicago"]`.

<br>

Then we will visit Portland's neighbor Kona and our visited list becomes `["Seattle", "Portland", "Chicago", "Kona"]`. Chicago doesn't have any unvisited neighbors, so our Breadth First is finished! 

<br>

Miami and El Paso are never visited because a basic breadth first search only visits nodes _reachable by the start node_. There is no path in the graph from Seattle to Miami or El Paso.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 37080b8b-47fc-468d-b47a-80451f736a26
* title: Breadth First Search on a Directed Graph
* points: 1

##### !question

Using the pseudocode included in the above lesson, if we begin our traversal from `Seattle`, what will a Breadth First Search return as its list of `visited` nodes for the following graph?

```python
    g = {
        "Seattle": ["Portland"],
        "Chicago": ["Seattle"],
        "Portland": ["Kona"],
        "Kona": []
    }
```

![Directed Graph](./images/directed-graph-example.png)

##### !end-question

##### !options

a| `visited = ["Seattle", "Chicago", "Portland", Kona"]`
b| `visited = ["Seattle", "Portland", "Chicago", Kona"]`
c| `visited = ["Seattle", "Chicago", "Portland"]`
d| `visited = ["Seattle", "Portland", "Kona"]`

##### !end-options

##### !answer

d|

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation 

Seattle will be added to visited first because Seattle is our specified start node. So visited is `["Seattle"]`.

<br>

We loop through Seattle's neighbors. Since the graph is provided as an adjacency dictionary, Seattle's neighbors are represented by `g["Seattle"]` which has value `["Portland"]`.  So we will visit Portland next and our visited list becomes `["Seattle", "Portland"]`.
<br>

Then we will visit Portland's neighbor Kona and our visited list becomes `["Seattle", "Portland", "Kona"]`.
<br>

There is an edge from Chicago to Seattle but there is no edge from Seattle to Chicago. Thus, Chicago is not reachable from Seattle and will never be visited during our breadth first search.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

Breadth first search is used to solve a variety of problems including:

- Checking to see if a graph is **connected** - we can get from any node in the graph to any other node in the graph
- Finding the shortest path in an unweighted graph/maze
- Solving puzzle games like a [Rubik's Cube](https://www.quora.com/How-can-solving-a-Rubiks-Cube-be-framed-as-a-graph-problem)

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 3398d942-7078-4567-9b81-67bb6c38d104
* title: Iterative Breadth First Search
* points: 1

##### !question

Write a function returning a list of elements representing a breadth first search of the items in the graph represented by `self.adjacency_list`. The traversal should begin with `start_node`. 

The function should return a list of all nodes reachable from `start_node` in the order they were traversed. If the graph is empty, the function should return an empty list. 

Spend no more then 15 minutes working through this independently. Use the hints below or reach out for help if you are still feeling stuck after 15 minutes. 

##### !end-question

##### !placeholder

```py
class Graph:
    
    # The graph is stored in an adjacency dictionary where each key 
    # represents a node in the graph and each value in the dictionary
    # represents the corresponding key's list of edges
    def __init__(self, adjacency_dict = {}):
        self.adjacency_dict = adjacency_dict

    def bfs(self, start_node):
        pass
```

##### !end-placeholder

##### !tests
```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_bfs(self):
        adjacency_dict = {
            "Seattle": ["Portland", "Chicago"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland"]
        }

        g = Graph(adjacency_dict)

        answer = ["Seattle", "Portland", "Chicago", "Kona"]
        self.assertEqual(answer, g.bfs("Seattle"))

    def test_bfs_empty_graph(self):
        g = Graph()
        self.assertEqual([], g.bfs("Seattle"))

    def test_bfs_one_item(self):
        adjacency_dict = {
            "Seattle": []
        }
        g = Graph(adjacency_dict)
        self.assertEqual(["Seattle"], g.bfs("Seattle"))
    
    def test_bfs_start_node_other_than_first_node(self):
        adjacency_dict = {
            "Seattle": ["Portland", "Chicago"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland"]
        }

        g = Graph(adjacency_dict)

        answer = ["Chicago", "Seattle", "Portland", "Kona"]
        self.assertEqual(answer, g.bfs("Chicago"))    


    def test_bfs_disconnected_graph(self):
        adjacency_dict = {
            "Seattle": ["Portland", "Chicago"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland"],
            "Miami": ["El Paso"],
            "El Paso": ["Miami"]
        }
        g = Graph(adjacency_dict)

        seattle_answer = ["Seattle", "Portland", "Chicago", "Kona"]
        self.assertEqual(seattle_answer, g.bfs("Seattle"))

        miami_answer = ["Miami", "El Paso"]
        self.assertEqual(miami_answer, g.bfs("Miami"))

    def test_bfs_directed_graph(self):
        adjacency_dict = {
            "Seattle": ["Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Kona"],
            "Kona": []
        }
        g = Graph(adjacency_dict)

        answer = ["Seattle", "Portland", "Kona"]
        self.assertEqual(answer, g.bfs("Seattle"))

```

##### !end-tests

##### !hint

Refer to the pseudocode included earlier in the topic to guide your implementation. 

Still feeling stuck? Check this video walkthrough of the solution.

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=42ac2142-176c-4846-8b69-af1d012341bf&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="360" width="640" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

### !end-hint

### !explanation 
An example of a working implementation:

```python
from collections import deque

def bfs(self, start_node):
    # store adjacency dictionary in variable for clarity
    graph = self.adjacency_dict
    
    # if there are no nodes in the graph
    if len(graph) == 0:
        # return an empty list
        return []
    
    # initialize a new queue and add start_node
    queue = deque([start_node])
    # initialize a list of visited nodes and add start_node
    visited = [start_node]
    
    # while there are still nodes int he queue
    while queue:
        # pop node off the queue and set it as current
        current = queue.popleft()
        
        # loop through current's neighbors
        for neighbor in graph[current]:
            # if the neighbor has not yet been visited
            if neighbor not in visited:
                # add it to the list of visited nodes
                # (we've now visited it!)
                visited.append(neighbor)
                # append the node to the queue so we can visit its neighbors!
                queue.append(neighbor)
    # return list of visited nodes
    return visited
```
### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 7b46c76f-c47e-4ed1-8606-732c610a1eaa
* title: Time complexity of BFS
* points: 1
* topics: graphs

##### !question

What is the time complexity of Breadth First Search with N nodes and E edges.

##### !end-question

##### !options

* O(N)
* O(N^2)
* O(E)
* O(NE)
* O(N + E)
* O(1)

##### !end-options

##### !answer

* O(N + E)

##### !end-answer

##### !explanation

Since we will visit each node in a connected graph once, and loop through each of the edges of each visited node the Big-O of this algorithm is O(N + E) where `N` is the number of nodes in the graph and `E` is the number of edges since each node and each edge will be explored.

O(N + E) is different from O(NE) because O(NE) implies that we visit each node `E` times. On the contrary, we visit each node at most one time, which is a set of operations resulting in a Big-O of O(N). We examine the edges adjacent to a node only when we visit the node, so each edge is examined at most two times, once for each of the nodes to which it is connected. This gives us a Big-O of O(2E) = O(E). Put together O(N) + O(E) and we get O(N + E).

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 4376fdea-ebec-4fdc-897d-21fc7ca5ff91
* title: Space Complexity of BFS
* points: 1
* topics: graphs

##### !question

What is the space complexity of Breadth First Search with N nodes and E edges?

##### !end-question

##### !options

* O(N)
* O(E)
* O(NE)
* O(N + E)
* O(1)


##### !end-options

##### !answer

* O(N)

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

In the worst-case you will need to add each node to the Queue, so the space complexity is O(N) where `N` is the number of nodes in the graph.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


### Depth First Search

Where breadth first search spreads out from a starting node in order of distance from the starting node, depth first search follows each path as far as possible before backing up and following the next closest path. For this reason we refer to depth first search as a _backtracking_ algorithm. Like breadth first search, a basic depth first search algorithm will only find nodes that can be reached from the start node.

We can imagine depth first search as if we were exploring a maze. Whenever there is a fork in the path, we make a choice about which fork to continue to travel down. If the fork we choose leads us to a dead-end (a node without unvisited neighbors), we turn around and go back to the most recent fork in the road, and choose one of the other options. 

![depth first search](images/dfs.gif)

In the above visualization, observe that the when the algorithm reaches node 3, it adds both of its neighbors (nodes 2 and 4) to the stack but does not yet consider its neighbors visited. It then chooses to visit the neighbor most recently added to the stack, node 4. Node 4's neighbor, node 5, is visited next. Then node 5's neighbor, node 6, is visited. And then node 6's neighbor node 7 is visited. It is only when it looks at node 7's neighbor, node 4, and realizes that node 4 has already been visited that it finally goes back and looks at node 3's second neighbor, node 2.  

The order in which depth first search traverses a graph's nodes can vary significantly if we switch the order in which we explore a node's neighbors. For example, if our algorithm instead added node 3's neighbors to the stack in the opposite order, the algorithm would traverse node 2 before node 4. It would then realize node 2 doesn't have any unvisited neighbors and proceed directly to node 4. The order in which nodes were visited would actually be the exact same as when we performed breadth first search. 

Neither depth first search nor breadth first search specifies the order in which we should explore a single node's neighbors. In most cases, we follow the order we find them in based upon the given graph representation. To access a node's neighbors in depth first search, we use the same representation-specific strategies discussed in the breadth first search section above.

To explore depth first search further, [HackerEarth](https://www.hackerearth.com/practice/algorithms/graphs/depth-first-search/visualize/) also has an excellent description and visualization of the algorithm.


**Depth First Search Pseudocode Walkthrough**
<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=8e2085ff-4dd1-46aa-a961-af170141a92a&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="360" width="640" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

The pseudocode for an iterative depth first search implementation is as follows:
```
- Start by taking the first item in the adjacency dictionary `start_node`
- Initialize an empty stack
- Initialize an empty list to store visited nodes
- Add the node we would like to start our traversal from to the stack
- while the stack is not empty:
    - Pop the topmost node off the stack and store it in a variable, `current`
    - If the node is not already in the list of visited nodes:
        - Add `current` to the list of visited nodes
    - Loop through the current node's neighbors:
        - If the neighbor has not yet been visited
            - Push the neighbor onto the stack
- Return list of visited nodes
```
<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: ebe508a4-d080-4176-9403-b9097e9a4009
* title: Three Node Cycle
* points: 1
<!-- * topics: [python, pandas] (Checkpoints only. optional the topics for analyzing points) -->

##### !question

Imagine that we change the pseudocode above to remove the line `If the node is not already in the list of visited nodes` before adding the current node to the list of visited nodes.

If we begin our traversal from `Miami`, what will this modified version of depth first search return as its list of `visited` nodes for the following graph?

```python
g = {
    "Miami": ["El Paso", "DC"],
    "El Paso": ["Miami", "DC"],
    "DC": ["Miami", "El Paso"]
}
```

![Three Node Graph](images/graph-cycle-example.png)


##### !end-question

##### !options

a| `visited = ["Miami", "DC", "El Paso"]`
b| `visited = ["Miami", "El Paso", "DC"]`
c| `visited = ["Miami", "DC", "El Paso", "El Paso"]`
d| `visited = ["Miami", "DC", "El Paso", "Miami"]`

##### !end-options

##### !answer

c|

##### !end-answer

<!-- other optional sections -->
##### !hint 
Draw out what is in the stack and in the list of visited node as you walk through the modified pseudocode line by line. 

##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation 
The answer is `visited = ["Miami", "DC", "El Paso", "El Paso"]`.

<br>

Miami is our start node so it gets added to our stack. Our stack is now `stack = ["Miami"]`. Then we begin our while loop and Miami is popped off the stack and added to our list of visited nodes. Our stack is now empty and `visited = ["Miami"]`.

<br>

We then loop through Miami's neighbors and add each unvisited neighbor to the stack. `g["Miami"]` gives us the value `["El Paso", "DC"]` so we add El Paso to the stack followed by DC. Our stack is now `stack = ["El Paso", "DC"]`. 

<br>

We begin another iteration through our while loop and pop the most recently appended item off the stack and set it as our current node. Thus DC becomes our current node. DC is added to visited. Now `visited = ["Miami", "DC"]`. 

<br>

We loop through DC's list of neighbors and add any unvisited neighbors to the stack. `g["DC"]` gives us the value `["Miami", "El Paso"]`. Miami is already in the list of visited nodes, but El Paso is not. This means that we end up adding El Paso to our stack twice: `stack = ["El Paso", "El Paso"]`. 

<br>

We iterate through the while loop again and remove the most recently appended El Paso from the stack and add it to the list of visited nodes. Now `stack = ["El Paso"]` and `visited = ["Miami", "DC", "El Paso"]`. We loop through El Paso's neighbors, but because El Paso's neighbors are all marked as visited, none of them get added to the list. 

<br>

However, there is still one El Paso remaining in the stack. So, we iterate through our while loop again. El Paso once again gets removed from the stack and added to visited. Now our stack is empty - `stack = []` but our visited list looks like `visited = ["Miami", "DC", "El Paso", "El Paso"]`. Removing the `if current not in visited` clause opens us up to potentially adding nodes to our visited list multiple times. 

##### !end-explanation 

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->



### !challenge

* type: multiple-choice
* id: b4aa5656-2b26-4e3d-a939-aa171975da65
* title: Depth First Search Traversal Order
* points: 1

##### !question

Using the iterative pseudocode included in the above lesson, if we begin our traversal from `Seattle`, what will a depth first search return as its list of `visited` nodes for the following graph?

```python
    g = {
        "Seattle": ["Chicago", "Portland"],
        "Chicago": ["Seattle"],
        "Portland": ["Seattle", "Kona"],
        "Kona": ["Portland", "Juneau"],
        "Juneau": ["Kona"]
    }
```
![DFS Example Graph](images/dfs-graph-example.png)
##### !end-question

##### !options


a| `visited = ["Seattle", "Chicago", "Portland", "Kona", "Juneau"]`
b| `visited = ["Seattle", "Portland", "Kona", "Juneau", "Chicago"]`
c| `visited = ["Seattle", "Chicago", "Portland", "Juneau", "Kona"`

##### !end-options

##### !answer

b|

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation 
Seattle is the given start node, so it is traversed and the list of visited nodes becomes `["Seattle"]`.

<br>

Next we loop through Seattle's neighbors `g["Seattle"]` which is the list `["Chicago", "Portland"]` and add them to the stack. Note that Chicago will be added to the stack followed by Portland. Stacks remove items in Last-In-First-Out order, so Portland will be the next node visited. Our list of visited nodes becomes `["Seattle", "Portland"]`. 

<br>

When we visit Portland, we'll add Portland's unvisited neighbor, Kona, to the stack. Kona is now the most recently added node in the stack, so it becomes the next node we pop off the stack and visit. The list of visited nodes becomes `["Seattle", "Portland", "Kona"]`. 

<br>

Then we add Kona's unvisited neighbor, Juneau, to the stack. Juneau is now the most recently added node in the stack, so it becomes the next node we pop off the stack and visit. The list of visited nodes becomes `["Seattle", "Portland", "Kona", "Juneau"]`.

<br>

Juneau doesn't have any unvisited neighbors so we look to see if there any remaining nodes in the stack. Chicago, Seattle's other neighbor, is still in the stack and unvisited! So it becomes the next node popped off the stack and our visited list becomes `["Seattle", "Portland", "Kona", "Juneau", "Chicago"]`. Our stack is now empty and our traversal is complete!
##### !end-explanation 

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

Depth first search has a number of applications in graph problems including:

- Checking if a graph is connected
- Detecting a cycle in a graph
- Finding a path in a maze where there is only one correct path
- Scheduling jobs based on dependencies on other jobs
  
<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: ce448643-59d9-44a8-b2c6-ba4a8a2227e5
* title: Iterative Depth First Search
* points: 1

##### !question

Write a function returning a list of elements representing a depth first search of the items in `self.adjacency_dict`. The traversal should begin with `start_node`. 

The function should return a list of all nodes reachable from `start_node` in the order they were traversed. If the graph is empty, the function should return an empty list. 

Please write the function iteratively, i.e. without using recursion.

Spend no more then 15 minutes working through this independently. Use the hints below or reach out for help if you are still feeling stuck after 15 minutes.

##### !end-question

##### !placeholder

```py
class Graph:
    
    # The graph is stored in an adjacency dictionary where each key 
    # represents an item in the graph and each value in the dictionary
    # corresponds to a list of edges from the key
    def __init__(self, adjacency_dict = {}):
        self.adjacency_dict = adjacency_dict

    def dfs(self, start_node):
        pass
```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_dfs(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland", "Juneau"],
            "Juneau": ["Kona"]
        }

        g = Graph(adjacency_dict)

        answer = ["Seattle", "Portland", "Kona", "Juneau", "Chicago"]
        self.assertEqual(answer, g.dfs("Seattle"))

    def test_dfs_empty_graph(self):
        g = Graph()
        self.assertEqual([], g.dfs("Seattle"))

    def test_dfs_one_item(self):
        adjacency_dict = {
            "Seattle": []
        }
        g = Graph(adjacency_dict)
        self.assertEqual(["Seattle"], g.dfs("Seattle"))

    def test_bfs_start_node_other_than_first_node(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland", "Juneau"],
            "Juneau": ["Kona"]
        }

        g = Graph(adjacency_dict)

        answer = ["Kona", "Juneau", "Portland", "Seattle", "Chicago"]
        self.assertEqual(answer, g.dfs("Kona"))    


    def test_dfs_disconnected_graph(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland", "Juneau"],
            "Juneau": ["Kona"],
            "Miami": ["El Paso", "Washington DC"],
            "El Paso": ["Miami", "Washington DC"],
            "Washington DC": ["Miami", "El Paso"]
        }
        g = Graph(adjacency_dict)

        seattle_answer = ["Seattle", "Portland", "Kona", "Juneau", "Chicago"]
        self.assertEqual(seattle_answer, g.dfs("Seattle"))

        miami_answer = ["Miami", "Washington DC", "El Paso"]
        self.assertEqual(miami_answer, g.dfs("Miami"))

    def test_dfs_directed_graph(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland"],
            "Juneau": ["Kona"]
        }
        g = Graph(adjacency_dict)

        answer = ["Seattle", "Portland", "Kona", "Chicago"]
        self.assertEqual(answer, g.dfs("Seattle"))
```

##### !end-tests

### !hint
Use the pseudocode included above this problem to guide your implementation. Observe that this is largely the same pseudocode as breadth first search except we use a stack in place of queue. We also change when we consider a node visited from when we first explore it as a neighbor to right after it becomes the current node. 

Still feeling stuck? Check this video walkthrough of the solution.

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=77eefecf-346b-4fe5-8b31-af1d0123414e&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="360" width="640" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

### !end-hint 

### !explanation
An example of a working implementation:

```python
from collections import deque
def dfs(self, start_node):
    # store adjacency dictionary in variable for clarity
    graph = self.adjacency_dict
    
    # if the graph is empty
    if len(graph) == 0:
        # return an empty list
        return []
    
    # initialize an stack and add the start node to it
    stack = deque([start_node])
    # create an empty list to store visited nodes
    visited = []

    # while the stack is not empty
    while stack:
        # pop the most recently added node off the stack and store it in current
        current = stack.pop()

        # if the current node hasn't yet been added to visited, add it
        if current not in visited:
            # add current to the list of visited nodes
            visited.append(current)

        # loop through current's neighbors
        for neighbor in graph[current]:
            # if the neighbor has not yet been visited
            if neighbor not in visited:
                # add the neighbor to the 'top' of the stack
                stack.append(neighbor)

    # return the list of visited nodes
    return visited
```
### !end-explanation

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### Stacks and recursion

Whenever we use a stack to solve a problem, the problem can often also be solved using recursion, especially when solution involves doing the same operation repeatedly. We can use the program's call stack to replace the explicit creation of a stack by using a recursive call. 

The pseudocode for the recursive implementation is as follows:
```
def dfs(self, start_node):
    - Create empty list to store visited nodes
    - Pass list of visited nodes and `start_node` into `dfs_helper`
    - Return list of visited nodes

- Helper function
def dfs_helper(self, start_node, visited)
    - If `start_node` is not in list of visited nodes
        - Append node to visited
        - Loop through the neighbors of the node
            - Call dfs_helper with list of visited nodes and the neighbor as the new start node
```

The key difference between our iterative and recursive implementations is that the explicit stack created in the iterative version is replaced by the recursive call stack.

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 95952a65-a741-48a1-969e-5d0d76f70c87
* title: Recursive DFS Traversal Order
* points: 1

##### !question

Using the recursive pseudocode included in the above lesson, if we begin our traversal from `Seattle`, what will a depth first search return as its list of `visited` nodes for the following graph?

```python
    g = {
        "Seattle": ["Chicago", "Portland"],
        "Chicago": ["Seattle"],
        "Portland": ["Seattle", "Kona"],
        "Kona": ["Portland", "Juneau"],
        "Juneau": ["Kona"]
    }
```
![DFS Example Graph](images/dfs-graph-example.png)
##### !end-question

##### !options


a| `visited = ["Seattle", "Chicago", "Portland", "Kona", "Juneau"]`
b| `visited = ["Seattle", "Portland", "Kona", "Juneau", "Chicago"]`
c| `visited = ["Seattle", "Chicago", "Portland", "Juneau", "Kona"`

##### !end-options

##### !answer

a|

##### !end-answer

<!-- other optional sections -->
##### !hint
In what order do we make recursive calls on a node's neighbors?
##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation 
Seattle is the given start node, so we make our initial call to our recursive helper function `dfs_helper("Seattle", [])` and within the recursive helper function, Seattle is added to our list of visited node. Thus visited is now assigned value `["Seattle"]`.

<br>

Next we loop through Seattle's neighbors `g["Seattle"]` which is the list `["Chicago", "Portland"]`. When we iterate over the neighbor Chicago, we call our recursive helper function and pass in Chicago as the new start node: `dfs_helper("Chicago", ["Seattle"])`.

<br>

When we enter our recursive helper function with Chicago as `start_node`, Chicago gets added to our list of visited nodes and now `visited = ["Seattle", "Chicago"]`. Chicago has no unvisited neighbors, so our recursive call `dfs_helper("Chicago", ["Seattle"])` finishes executing and we go back to our initial recursive call with Seattle as the starting node.

<br>

Within our `dfs_helper("Seattle", [])` call, we can now finish looping over Seattle's neighbors. Seattle's next unvisited neighbor is Portland, so we make a new recursive call `dfs_helper("Portland", ["Seattle, "Chicago"])`.

<br>

When we visit Portland, it gets added to the visited list and we'll make a new recursive call on Portland's only unvisited neighbor, Kona with `dfs_helper("Kona", ["Seattle", "Chicago", "Portland"])`.

<br>

Kona gets added to the list of visited nodes, and we make a recursive call on Kona's unvisited neighbor, Juneau: `dfs_helper("Juneau", ["Seattle", "Chicago", "Portland", "Kona"])`. 

<br>

Juneau is added to visited so now `visited = ["Seattle", "Chicago", "Portland", "Kona", "Juneau"]`. Juneau doesn't have any unvisited neighbors so we don't make any more recursive calls! There are no more unvisited neighbors of any nodes so our recursive calls get popped off the call stack until it is empty and our traversal is complete!

<br>
Take a look at the iterative version of this question asked earlier in the lesson and notice how creating an explicit stack instead of using the call stack changes the order in which a node's neighbors are explored!

##### !end-explanation 


### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 243eaf9a-e87e-48f6-bfa0-9df10c5b15d2
* title: Recursive Depth First Search
* points: 1

##### !question

Write a function returning a list of elements representing a depth first search of the items in `self.adjacency_dict`. Please write the function recursively.

Spend no more then 15 minutes working through this independently. Use the hints below or reach out for help if you are still feeling stuck after 15 minutes.

##### !end-question

##### !placeholder

```py
class Graph:
    
    # The graph is stored in an adjacency dictionary where each key 
    # represents an item in the graph and each value in the dictionary
    # corresponds to a list of edges from the key
    def __init__(self, adjacency_dict = {}):
        self.adjacency_dict = adjacency_dict

    def dfs(self, start_node):
        pass
```

##### !end-placeholder

##### !tests
```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_dfs(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland", "Juneau"],
            "Juneau": ["Kona"]
        }

        g = Graph(adjacency_dict)

        answer = ["Seattle", "Chicago", "Portland", "Kona", "Juneau"]
        self.assertEqual(answer, g.dfs("Seattle"))

    def test_dfs_empty_graph(self):
        g = Graph()
        self.assertEqual([], g.dfs("Seattle"))

    def test_dfs_one_item(self):
        adjacency_dict = {
            "Seattle": []
        }
        g = Graph(adjacency_dict)
        self.assertEqual(["Seattle"], g.dfs("Seattle"))

    def test_bfs_start_node_other_than_first_node(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland", "Juneau"],
            "Juneau": ["Kona"]
        }

        g = Graph(adjacency_dict)

        answer = ["Kona", "Portland", "Seattle", "Chicago", "Juneau"]
        self.assertEqual(answer, g.dfs("Kona"))    


    def test_dfs_disconnected_graph(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland", "Juneau"],
            "Juneau": ["Kona"],
            "Miami": ["El Paso", "Washington DC"],
            "El Paso": ["Miami", "Washington DC"],
            "Washington DC": ["Miami", "El Paso"]
        }
        g = Graph(adjacency_dict)

        seattle_answer = ["Seattle",  "Chicago", "Portland", "Kona", "Juneau"]
        self.assertEqual(seattle_answer, g.dfs("Seattle"))

        miami_answer = ["Miami", "El Paso", "Washington DC"]
        self.assertEqual(miami_answer, g.dfs("Miami"))

    def test_dfs_directed_graph(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Kona"],
            "Kona": ["Portland"],
            "Juneau": ["Kona"]
        }
        g = Graph(adjacency_dict)

        answer = ["Seattle", "Chicago", "Portland", "Kona"]
        self.assertEqual(answer, g.dfs("Seattle"))
```

##### !end-tests

##### !hint
Use the pseudocode above to guide your implementation.

Still feeling stuck? Check this video walkthrough of the solution.

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=25b3e12d-bc1a-40a5-b60c-af1d01234183&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="360" width="640" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

##### !end-hint 

##### !explanation
An example of a working implementation:

```python
# helper function
def dfs_helper(self, start_node, visited):
    # store adjacency_dict in variable 'graph' for clarity
    graph = self.adjacency_dict

    # if the node has not already been added to visited
    if start_node not in visited:
        # add the node to the list of visited nodes
        visited.append(start_node)
        # loop through the node's neighbors
        for neighbor in graph[start_node]:
            # call helper function with neighbor as new start node
            self.dfs_helper(neighbor, visited)



# driver function
def dfs(self, start_node):
    # store adjacency_dict in variable 'graph' for clarity
    graph = self.adjacency_dict

    # if the graph is empty
    if len(graph) == 0:
        # return an empty list
        return []

    # initialize a list to store visited nodes in
    visited = []

    # make initial call to recursive helper function
    # pass sin start_node and initialized visited list
    self.dfs_helper(start_node, visited)

    # return the list of visited nodes
    return visited
```

##### !end-explanation 

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 72fd7b4f-2d0b-4f60-9f99-57ede4dc769b
* title: Time complexity of DFS
* points: 1
* topics: graphs

##### !question

What is the time complexity of Depth First Search with N nodes and E edges?

##### !end-question

##### !options

* O(N)
* O(E)
* O(NE)
* O(N + E)
* O(1)


##### !end-options

##### !answer

* O(N + E)

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

Since you will visit each node once, and loop through each of the edges in each node the Big-O of this algorithm is O(N + E) where `N` is the number of nodes in the graph and `E` is the number of edges since each node and each edge will be explored.  Note, this is the same as breadth-first-search.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: ac56a302-147e-44bd-9438-3779d9fe226a
* title: Space complexity of DFS
* points: 1
* topics: graphs

##### !question

What is the space complexity of Depth First Search?

##### !end-question

##### !options

* O(N)
* O(E)
* O(NE)
* O(N + E)
* O(1)

##### !end-options

##### !answer

* O(N)

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

In the worst-case you will need to add each node to the Stack, so the space complexity is O(N) where `N` is the number of nodes in the graph.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->
## Choosing Between Traversal Algorithms

How do we decide which algorithm to use? Oftentimes, problems requiring graph traversal can be solved with either breadth first search or depth first search.

If we expect the solution to be relatively close to our start node, we may choose to breadth first search because it explores nodes closest to it first. Conversely, if we expect the solution to be much further away from the start node, we may choose to use depth first search. 

Breadth first search will also find the shortest path in an unweighted graph because it chooses which node to visit next based on proximity (first neighbors, then the neighbor's neighbors, etc.). 

Depth first search goes down one path as far as possible and only turns around and explores other possibilities only once it can't continue down the path its on. For this reason, depth first search is often used to solve problems where we want to test out different possible game outcomes or win conditions.

## Summary

Two popular graph traversal algorithms are breadth first search (BFS) and depth first search (DFS). Both algorithms will visit each node and edge in the graph, but they have different methods of performing the traversal. In most cases, both BFS and DFS can be used to solve a problem. However, there are instances in which the differences in approach make one a better choice than the other. The most common use cases for each are listed below. 

Breadth first search processes nodes by visiting all neighboring nodes before moving on to nodes that are neighbors of its neighbors and so-on.
Depth first search processes nodes by following a path as deep as it can before backing up and following another path.

**Breadth-first-search**|**Depth-first-search**|
:-----:|:-----:|
Typically implemented using a queue|Typically implemented using a stack|
Generally requires more memory than DFS|Generally requires less memory than BFS|
Optimal for finding the shortest distance of a path|Not optimal for finding the shortest distance|

**BFS Use Cases**|**DFS Use Cases**|
:-----:|:-----:|
Shortest path between two nodes|Detecting cycles in a graph|
Testing if a graph is bipartite|Problems that require graph backtracking|
Find all connected nodes in a graph|Topological sorting|
