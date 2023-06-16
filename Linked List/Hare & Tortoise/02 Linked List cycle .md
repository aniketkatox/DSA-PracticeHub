# Python Code

```python

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        """
        Determines whether a linked list contains a cycle.

        Args:
            head: The head of the linked list.

        Returns:
            True if a cycle is present in the linked list, False otherwise.
        """

        # Initialize both the turtle and hare pointers at the head of the linked list
        turtle = hare = head

        while hare and hare.next:
            # Move the hare pointer two steps ahead
            hare = hare.next.next
            # Move the turtle pointer one step ahead
            turtle = turtle.next
            
            # Check if the turtle and hare pointers meet
            if turtle == hare:
                # Cycle detected, return True
                return True

        # No cycle found, return False
        return False

```

**Time Complexity**
- The time complexity of the hasCycle function is O(n), where n is the number of nodes in the linked list. This is because in the worst case, we need to traverse the entire linked list to determine if a cycle exists. The while loop iterates at most n/2 times, so it can be considered as O(n) time complexity.

**Space Complexity**
- The space complexity is O(1) because the function uses only a constant amount of additional space to store the turtle and hare pointers. Regardless of the size of the linked list, the amount of extra space used remains the same.

# C++ Code

```cpp
class Solution {
public:
    /**
     * Checks if a linked list contains a cycle.
     * 
     * @param head The head of the linked list.
     * @return True if a cycle is present, False otherwise.
     */
    bool hasCycle(ListNode *head) {
        // If the list is empty, there can't be a cycle
        if (head == NULL) {
            return false;
        }

        ListNode *slow = head;
        ListNode *fast = head;

        // Move the slow pointer by one step and the fast pointer by two steps
        // If there is a cycle, the fast pointer will eventually catch up to the slow pointer
        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            
            // If the slow and fast pointers meet, a cycle is present
            if (slow == fast) {
                return true;
            }
        }
        // If the loop ends without the slow and fast pointers meeting, no cycle is present
        return false;
    }
};
```
