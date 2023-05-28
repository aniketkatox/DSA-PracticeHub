# Python Code

```python 

class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        """
        Reverses every K elements in a linked list.

        Args:
            head (ListNode): The head of the linked list.
            k (int): The group size for reversing.

        Returns:
            ListNode: The head of the modified linked list.
        """
        if not head or k == 1:
            return head

        dummyNode = ListNode(0)
        dummyNode.next = head
        currGroup = dummyNode

        while currGroup:
            currGroup = self.reverseNextK(currGroup, k)

        return dummyNode.next

    def reverseNextK(self, currGroup: ListNode, k: int) -> ListNode:
        """
        Reverses the next K elements of a linked list.

        Args:
            currGroup (ListNode): The node before the current group.
            k (int): The group size for reversing.

        Returns:
            ListNode: The node after reversing the current group.
        """
        lastNodeOfPrevGroup = currGroup
        initialFirstNodeOfCurrentGroup = currGroup.next

        # Check if there are enough nodes to reverse
        count = k
        while count > 0:
            currGroup = currGroup.next
            count -= 1
            if not currGroup:
                return None

        initialLastNodeOfCurrentGroup = currGroup
        firstNodeOfNextGroup = currGroup.next

        prevNode = None
        currNode = initialFirstNodeOfCurrentGroup

        # Reverse the current group
        while currNode != firstNodeOfNextGroup:
            nextNode = currNode.next
            currNode.next = prevNode
            prevNode = currNode
            currNode = nextNode

        # Connect the reversed group to the previous and next groups
        lastNodeOfPrevGroup.next = initialLastNodeOfCurrentGroup
        initialFirstNodeOfCurrentGroup.next = firstNodeOfNextGroup

        return initialFirstNodeOfCurrentGroup


```

**Time Complexity**
- The time complexity of the reverseKGroup function is O(n), where n is the total number of nodes in the linked list. This is because we need to traverse each node in the linked list once to reverse the groups.

**Space Complexity**
- The space complexity is O(1) because we are using a constant amount of extra space for variables, regardless of the size of the input linked list. We are not using any additional data structures that grow with the input size.
