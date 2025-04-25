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


### Short Answer Practice - Utility of Binary Search Trees
### !challenge

* type: paragraph
* id: ca15bd85-d63b-4197-8a44-5caeecec1b54
* title: Utility of Binary Search Trees

##### !question

In your own words, why are binary search trees useful? What is an example use case for binary search trees?

##### !end-question

##### !placeholder

Why BSTs?

##### !end-placeholder

### !end-challenge

### Short Answer Practice - Balanced Trees

### !challenge

* type: paragraph
* id: e7fd45e2-ec6a-4208-9682-8766406cb43f
* title: Why is it important for a tree to be balanced?
* points: 1
* topics: python, binary-search-trees

##### !question

Why is it so important for a binary search tree to be balanced?

##### !end-question

##### !placeholder

Why keep a tree balanced?

##### !end-placeholder

##### !explanation

A binary search tree maintains O(log n) time to find, add, and remove elements, *if and only if* the tree is balanced.  If the tree is not balanced then the time to find, add, and remove elements will resemble a be O(n).

##### !end-explanation

### !end-challenge


### Technical Practice - Height
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


### Technical Practice - Removal


### !challenge
* type: code-snippet
* language: python3.6
* id: e6e5ea66-d55f-4fc0-bc6f-eeda3f8106bd
* title: Binary Search Tree Recursive Removal
* points: 0

##### !question

Without looking back at the lesson's implementation, implement `delete` recursively for a binary search tree. The `key` is the key of the node the user wants to remove. If there are multiple nodes with the same key, `delete` should remove the first node in the tree with that key.

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
    
    def delete(self, key):
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
    def inorder_helper(self, current_node, values):
        if not current_node:
            return values
        self.inorder_helper(current_node.left, values)
        values.append({ 
            "key": current_node.key,
            "value": current_node.value
        })
        self.inorder_helper(current_node.right, values)
        return values
    def inorder(self):
        values = []
        return self.inorder_helper(self.root, values)
class TestPython1(unittest.TestCase):
    def setUp(self) -> None:
        def tree_with_nodes() -> TreeExtended():
            t = TreeExtended()
            t.add(5, "Peter")
            t.add(3, "Paul")
            t.add(1, "Mary")
            t.add(10, "Karla")
            t.add(9, "Mae")
            t.add(15, "Ada")
            t.add(13, "Nate")
            t.add(11, "Jane")
            t.add(12, "Jenny")
            t.add(25, "Kari")
            return t
        def tree_with_dupe() -> TreeExtended():
            t = TreeExtended()
            t.add(5, "Peter")
            t.add(3, "Paul")
            t.add(1, "Mary")
            t.add(5, "Peter's Twin")
            return t
        
        self.empty_tree = TreeExtended()
        self.tree_with_nodes = tree_with_nodes()
        self.tree_with_dupe = tree_with_dupe()
    
    def tearDown(self) -> None:
        self.empty_tree = TreeExtended()
    def test_returns_none_for_empty_tree(self):
        self.empty_tree.delete(5)
        self.assertEqual([], self.empty_tree.inorder())
    
    def test_can_remove_single_root_node(self):
        self.empty_tree.add(5, "Peter")
        self.empty_tree.delete(5)
        self.assertEqual([], self.empty_tree.inorder())
    def test_can_remove_left_leaf(self):
        self.empty_tree.add(5, "Peter")
        self.empty_tree.add(3, "Mary")
        expected = [{
            'key': 5,
            'value': 'Peter'
        }]
        self.empty_tree.delete(3)
        self.assertEqual(expected, self.empty_tree.inorder())
    
    def test_can_remove_right_leaf(self):
        self.empty_tree.add(5, "Peter")
        self.empty_tree.add(10, "Paul")
        expected = [{
            'key': 5,
            'value': 'Peter'
        }]
        self.empty_tree.delete(10)
        self.assertEqual(expected, self.empty_tree.inorder())
    def test_can_remove_node_with_two_children(self):
        self.empty_tree.add(5, "Peter")
        self.empty_tree.add(1, "Paul")
        self.empty_tree.add(10, "Mary")
        expected = [
            {
                'key': 1,
                'value': 'Paul'
            },
            {
                'key': 10,
                'value': 'Mary'
            }
        ]
        self.empty_tree.delete(5)
        self.assertEqual(expected, self.empty_tree.inorder())
    def test_can_find_inorder_successor(self):
        self.tree_with_nodes.delete(10)
        expected = [
            {
                'key': 1,
                'value': 'Mary'
            },
            {
                'key': 3,
                'value': 'Paul' 
            },
            {
                'key': 5,
                'value': 'Peter'
            },
            {
                'key': 9,
                'value': 'Mae'
            },
            {
                'key': 11,
                'value': 'Jane'
            },
            {
                'key': 12,
                'value': 'Jenny'
            },
            {
                'key': 13,
                'value': 'Nate'
            },
            {
                'key': 15,
                'value': 'Ada'
            },
            {
                'key': 25,
                'value': 'Kari'
            }
        ]
        self.assertEqual(expected, self.tree_with_nodes.inorder())
    def test_can_delete_dupe(self):
        self.tree_with_dupe.delete(5)
        expected = [
            {
                "key": 1,
                "value": "Mary"
            },
            {
                "key": 3,
                "value": "Paul"
            },
            {
                "key": 5,
                "value": "Peter's Twin"
            }
        ]
        self.assertEqual(expected, self.tree_with_dupe.inorder())
    def test_delete_does_not_crash_if_key_not_found(self):
        self.tree_with_nodes.delete(14)
        expected = [
            {"key": 1, "value": "Mary"},
            {"key": 3, "value": "Paul"},
            {"key": 5, "value": "Peter"},
            {"key": 9, "value": "Mae"},
            {"key": 10, "value": "Karla"},
            {"key": 11, "value": "Jane"},
            {"key": 12, "value": "Jenny"},
            {"key": 13, "value": "Nate"},
            {"key": 15, "value": "Ada"},
            {"key": 25, "value": "Kari"}
        ]
        self.assertEqual(expected, self.tree_with_nodes.inorder())
    
```

##### !end-tests

<!-- other optional sections -->
##### !hint 
Delete method pseudocode:
```txt
Base Case:
   - If the current root is None, return None

Recursive Case:
   - If the key is less than the current node's key:
       - Set current node’s left child to the result of calling the delete function on current node's left subtree.

   - If the key is greater than the current node's key:
       - Set current node’s right child to the result of calling the delete function on current node's right subtree.

   - If the key matches the current node’s key, we have found the node to delete:
       - If the current node doesn't have a left subtree
           - Return the right subtree

       - If the current node doesn't have a right subtree
           - Return the left subtree

       - If the current node has both left and right subtrees:
           - Find the minimum node in the right subtree 
               - Starting from the right subtree node, traverse the left nodes. The minimum node will be in last leaf of the left subtree of the node we started from.
           - Replace the key and value of the current node with the key and value of the minimum node found in the previous step
           - Remove the minimum node we found in the right subtree of the current node so we don’t have a duplicated node. Use the recursive delete function to remove the minimum node. 

   - Return the current node
```


Consider creating a helper function to find the minimum node in a tree. 

Still feeling stuck? Check this video walkthrough of the solution.

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=5e4deb73-094d-4c97-b2db-af0e0148f7f9&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="360" width="640" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>
##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation 
An example of a working implementation:

```py
def delete(self, key):
    # call our recursive helper on the root
    self.root = self.delete_helper(self.root, key)

# Recursive helper function
def delete_helper(self, current_root, key):
    # if the current node is None, the tree is empty 
    # or the key could not be found
    if not current_root:
        return None

    # if key is less than current node's call delete on left subtree
    if key < current_root.key:
        current_root.left = self.delete_helper(current_root.left, key)

    # if key is greater than current node's call delete on right subtree
    elif key > current_root.key:
        current_root.right = self.delete_helper(current_root.right, key)

    # if we found the node to delete
    else:
        # if node doesn't have a left subtree, 
        # return the right subtree
        if not current_root.left:
            return current_root.right

        # if node doesn't have a right subtree, 
        # return the left subtree
        elif not current_root.right:
            return current_root.left

        # if node has both left and right subtrees:
        # find the minimum node in the right subtree, 
        # and replace the deleted node with it
        current_root.key, current_root.value = self.min_node(current_root.right)
        # delete the minimum node in the right subtree
        current_root.right = self.delete_helper(current_root.right, current_root.key)

    # return the current node
    return current_root

# Helper function to find the minimum node in a tree
# minimum node will be in last leaf in left subtree
def min_node(self, root):
    # traverse left subtree by replacing root with left subtree
    while root.left:
        root = root.left

    # return the key and the value of minimum node
    return root.key, root.value
```

##### !end-explanation 
### !end-challenge

## Additional Resources
* [C16 Video Lessons](https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=ceac4982-192f-44a7-88a8-ad91016c972b)
* [C16 Slide Deck](https://docs.google.com/presentation/d/1M1tDoYMERJKwHBOp8LEmGDLwpg1kDqtGEpsGgrvPoIU/edit?usp=sharing)
* [Binary Search Tree Lecture using Ruby](https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=d9746397-8a10-43be-b1cc-aaaf00720b31)
* [Binary Search Trees with Ruby Slide Deck](https://docs.google.com/presentation/d/1Fj0deIUswGZ3ooJMpgVUqPEaWHKTkQ1w2Ci-yf8v66M/edit?usp=sharing)
* [MIT Open Courseware on Binary Search Trees](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-006-introduction-to-algorithms-fall-2011/lecture-videos/lecture-5-binary-search-trees-bst-sort/)
* [FreeCodeCamp Binary Search Tree Algorithms for JavaScript Beginners](https://www.freecodecamp.org/news/binary-tree-algorithms-for-javascript-beginners/)
* [Geeks for Geeks on Self-Balancing-Binary-Search-Trees](https://www.geeksforgeeks.org/self-balancing-binary-search-trees-comparisons/)
* [Dev Genius Depth First Search Tree Traversals](https://blog.devgenius.io/dfs-depth-first-search-traversal-techniques-short-and-sweet-1e4c134babcf)