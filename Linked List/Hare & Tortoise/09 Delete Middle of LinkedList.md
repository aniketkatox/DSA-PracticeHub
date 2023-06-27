# Java Code

```Java


class Solution {
    /**
     * Deletes the middle node from a linked list.
     *
     * @param head The head of the linked list.
     * @return The head of the modified linked list.
     */
    public ListNode deleteMiddle(ListNode head) {
        // Check if the list is empty or has only one node
        if (head == null || head.next == null) {
            return null; // No middle node to delete
        }

        ListNode turtle = head; // The slow pointer (turtle)
        ListNode hare = head; // The fast pointer (hare)
        ListNode prev = null; // The previous node of the turtle

        // Move the hare pointer two steps and the turtle pointer one step
        // When the hare pointer reaches the end, the turtle pointer will be at the middle
        while (hare != null && hare.next != null) {
            hare = hare.next.next;
            prev = turtle;
            turtle = turtle.next;
        }

        // Delete the middle node by updating the next reference of the previous node
        prev.next = turtle.next;

        return head;
    }
}
```

### Time Complexity
- The time complexity of the deleteMiddle method is O(n), where n is the number of nodes in the linked list. This is because we need to traverse the linked list to find the middle node. The traversal requires visiting each node once, resulting in a linear time complexity.

### Space Complexity
- The space complexity of the method is O(1), constant space. We are using a constant number of variables (turtle, hare, and prev) to keep track of the nodes during traversal and deletion. Regardless of the size of the linked list, the amount of additional space used remains constant, making it a constant space complexity.
