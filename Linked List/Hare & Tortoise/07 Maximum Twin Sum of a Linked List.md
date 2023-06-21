# Python
```python
class Solution:
    def pairSum(self, head: ListNode) -> int:
        """
        Calculates the maximum sum of pairs of values from the linked list.

        @param head: The head of the linked list.
        @return: The maximum sum of pairs of values.
        """
        slow = head
        fast = head

        # Find middle (slow) of the linked list
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # Reverse the second half of the linked list
        prevPtr = None
        currPtr = slow
        while currPtr:
            nextPtr = currPtr.next
            currPtr.next = prevPtr
            prevPtr = currPtr
            currPtr = nextPtr

        # Calculate the maximum pair sum
        leftPtr = head
        rightPtr = prevPtr
        maxSum = 0
        while rightPtr:
            maxSum = max(maxSum, leftPtr.val + rightPtr.val)
            leftPtr = leftPtr.next
            rightPtr = rightPtr.next

        return maxSum

```

**Time Complexity**
- The time complexity of the pairSum function is O(n), where n is the number of nodes in the linked list. The function first finds the middle of the linked list, which takes O(n/2) time. Then, it reverses the second half of the list, which takes O(n/2) time. Finally, it calculates the maximum pair sum by traversing both halves of the list, which also takes O(n/2) time. Therefore, the overall time complexity is O(n/2 + n/2 + n/2) = O(n).

**Space Complexity**
- The space complexity of the code is O(1) because it uses a constant amount of extra space, regardless of the size of the linked list.

# C++ Code
```cpp
class Solution {
public:
    /**
     * Calculates the maximum sum of pairs of values from a given linked list.
     *
     * @param head A pointer to the head node of the singly-linked list.
     * @return The maximum sum of pairs of values.
     */
    int pairSum(ListNode* head) {
        // Find the middle of the linked list
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast != nullptr && fast->next != nullptr) {
            slow = slow->next;
            fast = fast->next->next;
        }

        // Reverse the second half of the linked list
        ListNode* prevPtr = nullptr;
        ListNode* currPtr = slow;
        ListNode* nextPtr;
        while (currPtr != nullptr) {
            nextPtr = currPtr->next;
            currPtr->next = prevPtr;
            prevPtr = currPtr;
            currPtr = nextPtr;
        }

        // Calculate the maximum pair sum
        ListNode* leftPtr = head;
        ListNode* rightPtr = prevPtr;
        int maxSum = 0;
        while (rightPtr) {
            maxSum = max(maxSum, leftPtr->val + rightPtr->val);
            leftPtr = leftPtr->next;
            rightPtr = rightPtr->next;
        }
        return maxSum;
    }
};
```
