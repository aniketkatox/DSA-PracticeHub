# Python Code

```python 

class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        """
        Reverses a singly linked list and returns the new head.

        Args:
            head (Optional[ListNode]): The head of the linked list.

        Returns:
            Optional[ListNode]: The new head of the reversed linked list.
        """
        prev_node = None
        next_node = None
        current_node = head

        while current_node:
            next_node = current_node.next  # Store the next node
            current_node.next = prev_node  # Reverse the next pointer
            prev_node = current_node       # Move prev_node to current_node
            current_node = next_node       # Move current_node to next_node

        return prev_node


```

**Time Complexity**
- O(N), where N is the number of nodes in the linked list. The method iterates over each node once, performing constant-time operations for each node.

**Space Complexity**
- Space Complexity: O(1). The method uses a constant amount of extra space regardless of the size of the linked list. It only requires a few pointers (prev_node, next_node, and current_node) to perform the reversal in-place.
