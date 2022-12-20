# Recursion: A Crash Course

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=6c9b0e2a-6031-40a9-863b-af690172d08f&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Recursion Crash Course Slides
- [Slide Deck used for Recursion Crash Course](https://docs.google.com/presentation/d/1DrEy1sy7qt2vDp6gKSyuXOvni7NouxfHj6hFAKwYI4I/edit?usp=sharing)

## Array-to-BST Code Block (used at timestamp 24:00)
If you have the screen space available to do so, you can follow along to the whiteboard walkthrough at timestamp 24:00 using the code block below.

```py
class TreeNode:
    def __init__(self, value, left = None, right = None):
        self.val = value
        self.left = left
        self.right = right


def arr_to_bst(arr):
    if not arr:
        return None

    mid = (len(arr)) // 2

    root = TreeNode(arr[mid])
    root.left = arr_to_bst(arr[:mid])
    root.right = arr_to_bst(arr[mid + 1:])
    return root
```

## Python Tutor
- [Sorted Array to BST Recursive Function with Python Tutor](https://pythontutor.com/visualize.html#code=class%20TreeNode%3A%0A%20%20%20%20def%20__init__%28self,%20value,%20left%20%3D%20None,%20right%20%3D%20None%29%3A%0A%20%20%20%20%20%20%20%20self.val%20%3D%20value%0A%20%20%20%20%20%20%20%20self.left%20%3D%20left%0A%20%20%20%20%20%20%20%20self.right%20%3D%20right%0A%0A%0Adef%20arr_to_bst%28arr%29%3A%0A%20%20%20%20if%20not%20arr%3A%0A%20%20%20%20%20%20%20%20return%20None%0A%0A%20%20%20%20mid%20%3D%20%28len%28arr%29%29%20//%202%0A%0A%20%20%20%20root%20%3D%20TreeNode%28arr%5Bmid%5D%29%0A%20%20%20%20root.left%20%3D%20arr_to_bst%28arr%5B%3Amid%5D%29%0A%20%20%20%20root.right%20%3D%20arr_to_bst%28arr%5Bmid%20%2B%201%3A%5D%29%0A%20%20%20%20return%20root%0A%20%20%20%20%0Asorted_array%20%3D%20%5B4,%205,%2010,%2012,%2019,%2048%5D%0Aarr_to_bst%28sorted_array%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false
)

One can use Python Tutor to visualize what happens in the memory addresses of the Python program for recursive functions.
