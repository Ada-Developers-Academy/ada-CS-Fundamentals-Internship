# Resources

## Vocabulary and Synonyms

Below is a summary of vocab that we covered in this lesson.

| Vocab          | Definition                                                    | Synonyms  | How to Use in a Sentence                                                      |
| -------------- | ------------------------------------------------------------- | --------- | ----------------------------------------------------------------------------- |
| Linked List | A linear collection of data elements whose order is not given by their physical placement in memory.  Each element of the list contains a reference to the next element.     |       | "Because I wanted to add and remove elements to the front and rear, I used a linked list to store the data." |
| Tree      | A widely used abstract data type that simulates a hierarchical tree structure, with a root value and subtrees of children with a parent node, represented as a set of linked nodes. |  | "I used a tree to store ordered data." |
| Binary Tree      | A tree structure in which each node has at most two children, which are referred to as the _left child_ and _right child_. |  | "A Mathematical expression can be written as a binary tree where the leaves are values and the parent nodes are operators like +, -, *, and /." |
| Binary Search Tree      | A specific type of Binary Tree which is a rooted binary tree data structure whose internal nodes each store a key greater than all the keys in the node’s left subtree and less than those in its right subtree. | Ordered Binary Tree | "Because 23 is less than the root, it can only be found in the left subtree of this binary search tree." |
| Leaf      | A node in a tree with no descendants. |  | "Because the left and right subtrees of the current node were `None`, this node is a leaf." |
| Parent      | A node with descendants. |  | "Because the left and right subtrees of the current node not `None`, this node is a parent and not a leaf." |
| Unbalanced Tree 	|  A BST where each node has 0 or 1 children (it looks like a linked list) 	| | The tree was unbalanced so inserting new values took linear time. |
| Balanced Tree 	| A tree where the the level of any two leaves differs by at most 1 node.	| | "Because my tree is balanced, it's quick to find values inside it."  |
| Subtree | The tree which is a child of a node. Note: The name emphasizes that everything which is a descendant of a tree node is a tree, too, and is a subset of the larger tree.| | "The value I'm looking for is less than the current node, so I will continue searching in the left subtree." |
| Traversal 	|  A method of visiting each node in a BST	| | "My method performs a traversal visiting each node in the tree, level-by-level." |
| Depth-First Traversal 	|  An algorithm for traversing or searching a tree. The algorithm starts at the root node and explores as far as possible along each branch before backtracking.	| | A depth-first traversal looks like a mouse exploring a maze in that it goes as far down one path before backtracking when encountering dead ends. |
| Breadth-first traversal 	|  An algorithm for searching a tree data structure for a node that satisfies a given property. It starts at the tree root and explores all nodes at the present depth prior to moving on to the nodes at the next depth level. 	| | I printed out the tree level-by-level so I had to perform a breadth-first traversal. |

## Optional - Additional Exercises

### Height
<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: a8078856-e772-4e3f-9267-6bbeb006ee5d
* title: Binary Search Tree Recursive Height
* points: 0

##### !question

Implement a recursive `height` function for a binary search tree. The function should return the height of the tree. Note that the tree may not be balanced. 

##### !end-question

##### !placeholder

```py
class TreeNode:
    def __init__(self, key, val = None):
        if val == None:
            val = key

        self.key = key
        self.value = val
        self.left = None
        self.right = None

class Tree:
    def __init__(self):
        self.root = None
    
    def height(self):
        # implement using recursion
        pass
```

##### !end-placeholder

##### !tests
```py
import unittest
from main import *

class TreeExtended(Tree):

    def add_helper(self, current_node, new_node):
        if new_node.key  < current_node.key:
            if not current_node.left:
                current_node.left = new_node
                return
            self.add_helper(current_node.left, new_node)
        else:
            if not current_node.right:
                current_node.right = new_node
                return
            self.add_helper(current_node.right, new_node)

    def add(self, key, value = None):
        if not self.root:
            self.root = TreeNode(key, value)
        else:
            new_node = TreeNode(key, value)
            self.add_helper(self.root, new_node)

class TestPython1(unittest.TestCase):
  def setUp(self) -> None:

    def tree_with_nodes() -> TreeExtended():
        t = TreeExtended()
        t.add(5, "Peter")
        t.add(3, "Paul")
        t.add(1, "Mary")
        t.add(10, "Karla")
        t.add(15, "Ada")
        t.add(25, "Kari")
        return t
    
    self.empty_tree = TreeExtended()
    self.tree_with_nodes = tree_with_nodes()
    
  def tearDown(self) -> None:
      self.empty_tree = TreeExtended()

  def test_height_of_empty_tree_is_zero(self):
    self.assertEqual(0,self.empty_tree.height())
  
  def test_height_of_one_node_tree_is_one(self):
    self.empty_tree.add(5, "Peter")

    self.assertEqual(1, self.empty_tree.height())

  def test_height_of_many_node_tree(self):
    self.assertEqual(4, self.tree_with_nodes.height())

    self.tree_with_nodes.add(2, "pasta")
    self.tree_with_nodes.add(2.5, "bread")
    self.assertEqual(5, self.tree_with_nodes.height())

```

##### !end-tests

<!-- other optional sections -->
##### !hint
Pseudocode:
```
If the current node is nil return 0

Otherwise return 1 plus the maximum of the heights of the right and left subtrees
```

Still feeling stuck? Check this video walkthrough of the solution.

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=996e137b-e4f2-460e-a2e8-af0e01521de6&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="360" width="640" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

##### !end-hint
##### !explanation 
An example of a working implementation:
```py
    def height_helper(self, current_node):
        if not current_node:
            return 0

        return max(self.height_helper(current_node.left), self.height_helper(current_node.right)) + 1
    
    def height(self):
        return self.height_helper(self.root)
```

##### !end-explanation


### !end-challenge

## Additional Resources

* [MIT Open Courseware on Binary Search Trees](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-006-introduction-to-algorithms-fall-2011/lecture-videos/lecture-5-binary-search-trees-bst-sort/)
* [FreeCodeCamp Binary Search Tree Algorithms for JavaScript Beginners](https://www.freecodecamp.org/news/binary-tree-algorithms-for-javascript-beginners/)
* [Geeks for Geeks on Self-Balancing-Binary-Search-Trees](https://www.geeksforgeeks.org/self-balancing-binary-search-trees-comparisons/)
*[Dev Genius Depth First Search Tree Traversals](https://blog.devgenius.io/dfs-depth-first-search-traversal-techniques-short-and-sweet-1e4c134babcf)