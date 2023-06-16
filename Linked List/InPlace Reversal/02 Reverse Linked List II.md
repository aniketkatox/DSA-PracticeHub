# Python Code

```python 

class Solution:
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        """
        Reverses a portion of a singly linked list specified by the left and right indices.

        Args:
            head (Optional[ListNode]): The head of the linked list.
            left (int): The left index indicating the start of the reversal.
            right (int): The right index indicating the end of the reversal.

        Returns:
            Optional[ListNode]: The head of the reversed linked list.
        """
        if not head or left == right:
            return head
        
        # Dummy node to handle the case when left = 1
        dummy = ListNode(0)
        dummy.next = head
        
        # Move to the node just before the reversal starts
        prev = dummy
        for _ in range(left - 1):
            prev = prev.next
        
        # Perform the reversal within the specified range
        curr = prev.next
        for _ in range(right - left):
            next_node = curr.next
            curr.next = next_node.next
            next_node.next = prev.next
            prev.next = next_node
        
        return dummy.next


```

**Time Complexity:** 
- O(N), where N is the number of nodes in the linked list. The algorithm requires a single pass through the linked list to reverse the specified portion.

**Space Complexity**
- Space Complexity: O(1). The algorithm uses a constant amount of extra space, regardless of the size of the linked list.

# C++ Code
```cpp
class Solution {
public:
    /**
     * Reverses a portion of a singly linked list specified by the left and right indices.
     * 
     * @param head The head of the linked list.
     * @param left The left index indicating the start of the reversal.
     * @param right The right index indicating the end of the reversal.
     * @return The head of the reversed linked list.
     */
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        // Dummy node to handle the case when left = 1
        ListNode* dummy = new ListNode(0, head);

        // (1) Reach the node at position "left"
        ListNode* curr = head;
        ListNode* left_prev = dummy;
        for (int i = 1; i <= left - 1; i++) {
            left_prev = left_prev->next;
            curr = curr->next;
        }

        // Now curr = "left" and left_prev is a node before curr
        // (2) Reverse from left to right
        ListNode* prev = nullptr;
        ListNode* nextptr;
        for (int i = 1; i <= right - left + 1; i++) {
            nextptr = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextptr;
        }

        // (3) Update the pointers
        left_prev->next->next = curr;
        left_prev->next = prev;

        return dummy->next;
    }
};
```
