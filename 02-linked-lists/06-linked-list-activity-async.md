# Additional Practice

## Rotate a Linked List

Consider the operations and implementation necessary to rotate a linked list, then implement the `add_first` and `get_last_two_nodes` helper functions used in the `rotate_list` function.

Tests are included in the repo to help you test whether your helper functions work correctly.

As always, if you are feeling stuck, we invite you to come to office hours, ask questions in Slack in #study-hall, or consult an AI tool to help you brainstorm an approach without providing a solution.

### Class Livecode Recording

Follow along with the [Class Discussions](./07-linked-lists-class-discussions.md) recording in the following repo as we livecode the `rotate_list` function in class: 
* [Rotate Linked List](https://github.com/Ada-Activities/rotate_linked_lists)
* Check out the `solution` branch in the repo to see a completed implementation of both the livecode and activity

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=53490d78-0856-4002-9215-afce01547022&autoplay=false&offerviewer=true&showtitle=true&showbrand=true&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

The repo `main` branch does not include the implementation of `rotate_list`. Try coding it along with the recording as you think about the steps needed to rotate a linked list. Before moving on to main activity work, you can either copy in the `rotate_list` implementation from the `solution` branch or from the section below.

<br>
<details style="max-width: 700px; margin: auto;">
  <summary><code>rotate_list</code> Implementation</summary>

```python
def rotate_list(head, k):
    # if the list does not exist, return None
    if not head:
        return None

    # if k < 0, raise an error
    if k < 0:
        raise ValueError("k must be greater than or equal to 0")
    
    # if k is 0 or if the list has one element, return the head of the list
    elif k == 0 or head.next is None:
        return head

    # loop k times
    for i in range(k):
        # set the new tail and new head to the last two nodes of the list
        new_tail, new_head = get_last_two_nodes(head)
        # the new tail's next reference will now be set to None
        new_tail.next = None
        # the head of the list is set to the old tail (new head)
        head = add_first(head, new_head)
    # after making k rotations, return the new head of the list
    return head
```

</details>

### Independent or Small Group Work

Feel free to complete this activity independently or in small groups. If you are working in a small group, have one person fork and clone the repository so that you can all work together on the implementation of the helper functions. Invite the other members of your group to the repo so that you can all push changes to the same repo and see each other's work.

- Time box no more than twenty minutes per function implementing a solution to the two helper functions using pseudocode or Python. 
- If you feel stuck, start by thinking about how you would solve the helper functions using pen and paper.
- Explain what is making you feel stuck and try to work through your questions with others!

### Solution

After you have had a chance to work on your own solution(s) for the `add_first` and `get_last_two_nodes` functions, check out the `solution` branch to see our working implementation:

* [Rotate Linked List Solution](https://github.com/Ada-Activities/rotate_linked_lists/blob/solution)

## Previous Recordings 

To see all the recordings related to Linked Lists, please consult the [Class Discussion](./07-linked-lists-class-discussions.md) section of this topic.