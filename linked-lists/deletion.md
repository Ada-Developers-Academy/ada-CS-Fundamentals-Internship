# Deletion

## `delete_at_head`


## `delete_at_index`: Removing a node at a specific index

To remove a node at a specific index, you first have to traverse the list until you find the index before the node to delete.  If the node to remove is the head, then the head becomes the next element.  Then adjust the prior node's `next` reference to point **past** the node you are removing.  

![remove a node #1](images/remove-node-1.png)
![remove a node #2](images/remove-node-2.png)
![remove a node #3](images/remove-node-3.png)
![remove a node #4](images/remove-node-4.png)

```python
def remove(self, index):
    if not self.head:
        return

    if index == 0:
        self.head = self.head.next

    # Traverse the list until you find the node at index -1
    current = self.head
    current_index = 0
    while current.next and current_index < index - 1:
        current = current.next
        current_index += 1

    # If the node exists
    if current.next:
        current.next = current.next.next
```


## `delete_by_value` (code challenge)