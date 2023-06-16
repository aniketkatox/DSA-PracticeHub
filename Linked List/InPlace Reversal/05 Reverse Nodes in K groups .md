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

# C++ Code
```cpp
class Solution {
public:
    /**
     * Reverses every K elements in a linked list.
     *
     * @param head The head of the linked list.
     * @param k The group size for reversing.
     * @return The head of the modified linked list.
     */
    ListNode* reverseKGroup(ListNode* head, int k) {
        if (head->next == NULL || k == 1) { // Base Case
            return head;
        }

        int size = 0;
        ListNode* temp = head;
        while (temp != NULL) {
            size++;
            temp = temp->next;
        }

        int count = size / k; // Number of groups to be reversed
        ListNode* dummy = new ListNode(0, head); // Create a dummy node to handle the modified list
        ListNode* prev1 = dummy;
        ListNode* curr1 = head;

        while (count) {
            // Set iterators to reach/link the next group
            int x = k - 1; // To reach the next group
            temp = curr1;
            while (x) {
                temp = temp->next;
                x--;
            }
            ListNode* prev2 = temp;
            ListNode* curr2 = temp->next;

            // Reverse the current group
            ListNode* prevptr = NULL;
            ListNode* currptr = curr1;
            ListNode* nextptr;

            while (currptr != curr2) {
                nextptr = currptr->next;
                currptr->next = prevptr;
                prevptr = currptr;
                currptr = nextptr;
            }

            // Adjust the links
            prev1->next = prev2;
            curr1->next = curr2;

            // Move iterators for the next iteration
            prev1 = curr1;
            curr1 = curr1->next;

            count--;
        }
        return dummy->next;
    }
};
```
