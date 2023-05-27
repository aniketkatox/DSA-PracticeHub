# Python Code

```python

class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        """
        Finds the middle node of a linked list.

        Args:
            head: The head node of the linked list.

        Returns:
            The middle node of the linked list.

        """
        turtle = hare = head

        # Move the turtle one step and the hare two steps at a time until the hare reaches the end
        while hare and hare.next:
            turtle = turtle.next
            hare = hare.next.next

        return turtle


```

**Time Complexity**
- The time complexity of the algorithm is O(n), where n is the number of nodes in the linked list. We traverse the linked list once, and the hare moves twice as fast, so the algorithm terminates in approximately n/2 steps.

**Space Complexity**
- The space complexity is O(1) since we are using only two additional pointers, turtle and hare, to find the middle node. The space usage remains constant regardless of the size of the linked list.
