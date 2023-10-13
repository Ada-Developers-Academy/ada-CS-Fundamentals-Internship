# Graph Application - Maze Solving

<!--
<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=6e2b199d-f7d8-4899-b750-afdc000581be&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>
-->

## Overview

Rarely do we need to search through a graph just for the sake of searching. Instead, we use graphs to model real-world problems and then use graph algorithms to solve those problems. Often, additional data will need to be carried along with the graph, and the graph algorithms will need to be modified to take advantage of that data. In this lesson, we'll look at one way that graph searching with additional data can be used to solve problems.

## Maze Solving

Some of graph examples we have already seen involved places. Each node represented a city and each edge represented a road or other mode of transportation between the two connected cities. But why restrict ourselves to the scale of cities?

We could make the graph nodes represent city blocks, intersections, or even arbitrarily small areas of space, such as every 1 square meter area of floor in our home. Areas with no obstructions between them (such as a wall) could then be connected by edges. In this way we could build a graph representation of the entire world, or at least a small part of it.

For the moment, let's restrict our attention to something slightly smaller than the entire world. We could use a graph to represent a maze, where each node represents a small location in the maze and each edge represents a path between two locations. Representing the maze this way, we could solve the maze by searching for a path of connected nodes from the start of the maze to the end.

Thus far, we have only considered the _mechanics_ of searching algorithms, and the resulting order they would visit the nodes in a graph. Now, we will examine how we can use our ability to visit the nodes of a graph to discover a path through the maze. To do so, we will need to consider how to represent the terrain of the maze, how to represent the maze as a graph, and how to modify our search algorithms to find a path through the maze.

### Maze Representation

There's no universal standard for how to describe a maze to a computer. The requirements of the description will vary based on the features of the maze. Is it curvy? Is it boxy (more formally we might say rectilinear)? Is it multi-level (overlapping)?

![Three rectilinear mazes. Maze A is 3 by 3 with a simple path through. Maze B is 10 by 5 with a slightly more circuitous path. Maze C is 30 by 10 with a complex path.](images/graphs_application_mazes.png)  
*Fig. Three rectilinear mazes of varying complexity.*

We'll keep things uncomplicated and restrict our mazes to a single level, rectilinear maze. There will be a single starting location, and single exit. We could use text, an image, or even a 3D model to describe the maze, but for our purposes, text will be the easiest to work with.

Consider the first maze depicted above. We can describe it as a series of rows and columns, where each cell is either a wall or a passage. We could use the following structure to describe the maze:

```py
maze_a = [
    "  #",
    "# #",
    "#  ",
]
```

Each character represents a cell in the maze. A space represents a passage, and a `#` represents a wall. The first row of the maze is represented by the first string in the list, the second row by the second string, and so on.

The other mazes can also be represented with this structure as shown below:

```py
maze_b = [
    "    #     ",
    " ## # # # ",
    " #  # ### ",
    " #### #   ",
    "      # # ",
]

maze_c = [
    "      #         #            #",
    "##### # ####### # ########## #",
    "## ## #       # #            #",
    "## ## #### #### ###### #######",
    "         # #        ## # #    ",
    "## ## #### #### ### ## # ## # ",
    "## ####### #### #         # # ",
    "              # ### ## # ## # ",
    "## ####### ######## ## # ## # ",
    "## #       #        ## #    # ",
]
```

One point to note is that the representations above do not explicitly indicate the start and end of the maze. We could add additional information to the representation to indicate the start and end (perhaps the start and end could be marked with "S" and "E" characters), but for now, we'll assume that information will be provided to us separately, such as tuples indicating the row and column of the start and end positions.

### Representing a Maze as a Graph

To find a path through the maze, we could absolutely work directly with the maze representation above. But it would be more convenient to convert the maze into a graph representation first. While this may seem more complicated, the benefit is that it allows us to separate the concern of processing this data representation from the concern of searching the graph.

In some ways, the maze representation is _already_ a graph, though in a non-standard layout. Each location acts as a node, and each has up to 4 neighbors (excluding diagonals) to its adjacent locations. But there are some complications.

First, the adjacency information exists only implicitly. Given a location composed of a row and column location `(r, c)`, we need to inspect each of the four adjacent locations by calculating them from the current location. Locations on the edges and corners of the maze will have fewer than four potential neighbors. We could account for this while also looking for a path through the maze (we need to account for this one way or another), but addressing this first will make the search algorithm simpler.

Second, when turning the maze representation into a graph, we need only represent the actual passage areas of the maze. A path through the maze cannot pass through walls, meaning the walls are not relevant to the search, and so we can ignore them. This will make the graph representation smaller and easier to work with.

To address these issues, we will create a new graph representation of the maze. In previous examples, we have used a string or a number to identify each node in our adjacency information. In this case, we will use a tuple of two numbers, representing the row and column of the location in the maze. We will still use a dictionary to represent the adjacency information. The keys of the dictionary will be the nodes, and the values will be a list of the nodes that are adjacent to the node represented by the key. In other words, we will construct an adjacency list representation of the maze corridors.

![Three representations of the 3 by 3 maze presented earlier. The grid representation represents the walls and corridors spatially. The node representation labels each corridor by location, and connects each to the immediately reachable adjacent corridors. Here, the nodes are arranged in the same shape as the original maze, though they could just as readily have been arranged in a straight line. The adjacency list depicts how we would expect the nodes to be represented using a python dictionary as described.](images/graphs_application_maze_to_graph.png)  
*Fig. Representing a maze as (a) a grid, (b) a collection of nodes, and as (c) an adjacency list. A lot of the code that programmers write relates to converting among various data representations.*  

<br />

<details style="max-width: 700px; margin: auto;">
  <summary>Click here to see the adjacency list source as text.</summary>

```py
graph = {
    (0, 0): [(0, 1)],
    (0, 1): [(0, 0), (1, 1)],
    (1, 1): [(0, 1), (2, 1)],
    (2, 1): [(1, 1), (2, 2)],
    (2, 2): [(2, 1)],
}
```

</details>

There are a few ways we could process the grid representation. Assuming we write a function `convert_maze_to_graph` that takes a maze grid `maze` as input and returns an adjacency list of nodes, represented by a tuple of its row and column, and the list of adjacent nodes, think about what the steps to convert the maze to a graph might be. Then take a look at our steps!

<br />

<details style="max-width: 700px; margin: auto;">
  <summary>Click here to see our steps!</summary>

1. Create an empty dictionary to hold the adjacency information.
2. Iterate over each row in the maze.
3. Iterate over each column in the row.
4. If the current cell is a wall, skip it, since the path cannot pass through a wall.
5. Otherwise, create a tuple representing the current cell `(r, c)`.
6. Create an empty list to hold the adjacent nodes.
7. For each of the four directions (up, right, down, left):
    1. Calculate the row and column of the adjacent cell.
    2. If the adjacent cell is out of bounds or a wall, skip it.
    3. Otherwise, create a tuple representing the adjacent cell.
    4. Add the tuple to the list of adjacent nodes.
8. Add the tuple and list of adjacent nodes to the dictionary.
9. Return the dictionary.

</details>

![A grid laid over the top-left corner marked (A) shows that the space to the left and above are invalid (outside the maze representation), while the spaces to the right and below are valid. A grid laid over a space along the top edge marked (B) shows that only the space above is invalid.](images/graphs_application_maze_corner_edge.png)  
*Fig. (A) has no location above or to the left in our maze representation. (B) has no location above it. Locations in the other corners and along the other edges have similar restrictions. We must inspect all of the neighbor locations, looking for a passage or a wall, and use that information to build a graph of the connected passage areas.*

Using those steps as a guide, think about how to write the function. Then take a look at our implementation! Notice that checking the directions around each node has the complication of needing to handle the case of the adjacent cell being out of bounds. We could simplify our main code by using a helper function to look up the value of the cell at the given row and column. If the row or column is out of bounds, we can treat it as though it were a wall. Then our main direction-handling code can be simplified to just checking whether or not the cell is a wall.

<br />

<details style="max-width: 700px; margin: auto;">
  <summary>Click here to see our implementation!</summary>

```py
# constants representing the walls and corridor
MAZE_WALL = "#"
MAZE_CORRIDOR = " "

# Builds an adjacency-list based graph from a grid-based maze representation.
def convert_maze_to_graph(maze):
    graph = {}

    # iterate over all the cells in the grid
    for r in range(len(maze)):
        for c in range(len(maze[0])):
            # skip this cell if it's not a corridor
            if maze[r][c] != MAZE_CORRIDOR:
                continue

            cell = (r, c)

            # Which directions can we move in?
            # Check each of the 4 locations by using a delta row and delta 
            # column pair. Delta typically refers to a change in a value, so 
            # here, dr is the delta row, the change in value of the row, and dc 
            # is the delta column, the change in value of the column.
            directions = []
            for dr, dc in ((-1, 0), (0, 1), (1, 0), (0, -1)):
                loc = (cell[0] + dr, cell[1] + dc)  # neighbor location

                # Use a helper to get the location value, treating invalid 
                # locations (outside the grid) as though they were walls
                if cell_lookup(maze, loc[0], loc[1]) == MAZE_CORRIDOR:
                    # Add this computed location to the valid directions from
                    # current cell
                    directions.append(loc)

            # Add the cell and its directions to the graph
            graph[cell] = directions

    return graph

# Helper method to safely get the value for the cell at the supplied row and
# columns. Invalid locations (outside the grid) are treated as walls.
def cell_lookup(maze, r, c):
    if r < 0 or r >= len(maze):
        return MAZE_WALL
    
    row = maze[r]
    if c < 0 or c >= len(row):
        return MAZE_WALL
    
    return row[c]
```

</details>

### Building a Path

Now that we have a graph representation of the maze, we actually already know everything we need to determine whether we _can_ reach the end of the maze. We can use any of the search approaches we have already seen to determine whether there is a path from the start to the end of the maze. Assuming we're told the start and the end node locations, then if we start searching through the graph from the start node and eventually visit the end node, there is a path! But what if we want to know _what_ the path is?

A later topic will cover finding the shortest path through a graph using breadth first search aided by some intermediate calculations. But for now, let's consider how we might find _some_ path through the maze. Assuming there is only a single path through the maze, then any search approach will find that same single path.

Let's use depth first search, modifying it slightly so that we can keep track of the path we have taken so far. Recursive depth first search is a convenient choice, since the calls it makes while moving through the graph follow a single path at a time. We can use this to our advantage by keeping track of the path it has taken so far, and then adding the current node to the path before continuing the search. If we reach the end of the maze, we will have a path from the start to the end. In contrast, breadth first search or iterative depth first search track a list of pending nodes. Each pending node may belong to a different path, so it would be more challenging to keep track of the path taken so far.

There is still one complication. Mazes have dead ends. What should we do with if we have been tracking our path, but then encounter a dead end? We could simply stop the search, but that would mean we would never find a path through the maze. Instead, we need to **backtrack**. We need to remove the last node from the path, and then continue the search from the previous node. If we reach a dead end again, we need to backtrack again. We need to keep backtracking until we find a node that has an unvisited neighbor. Then we can continue the search from that node.

![A small maze that may require backtracking to solve. The node representation is animated according to how nodes are visited, and the visited and path lists are displayed.](images/graphs_application_maze_backtrack.webp)  
*Fig. A small maze with a dead end, requiring backtracking to move back to the last decision point where the next unvisited node can be reached. The grid representation depicts the exploration path as an arrow, and the red portion is where backtracking occurs. The node representation shows the how the visited list and path are tracked as the end is searched for.*  

A recursive depth first search works very well for this situation. As we recurse our way through the graph, we can add the current node to our path. If we reach a dead end (a node with no unvisited neighbors), we can remove the node from the end of the path, then `return` to the previous node, where can resume iterating over _its_ neighbors.

<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-info

## Other Path Finding Approaches Are Possible

As we become more comfortable with graphs, we might think about how iterative depth first search or breadth first search could also be modified to find a path through the maze. Since the pending list of nodes in these approaches can contain nodes from multiple paths, it's more challenging to know whether the next node to visit is part of the current path or a different path. Tracking additional data for each node, such as its distance from the start of the path (equivalent to the depth of the call stack in our example), or the node that led to it, can help us determine whether we've switched paths, or could even be used to reconstruct the path once we reach the end of the maze.

<br />

For the moment, we don't recommend spending too much time delving into these other approaches, but it's worth coming back to this topic later, once we've had more practice with graphs.

### !end-callout

If we reach the end of the maze, we can return the path, and the search will unwind, returning the path from the previous node, and so on, until we reach the start of the maze, and our full path is returned.

### Limitations

### Complexity

## Summary




