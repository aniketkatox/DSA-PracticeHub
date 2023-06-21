# Python
```python
class Node:
    def __init__(self, val):
        """
        Constructor to initialize a new Node object.

        Args:
            val: The value to be stored in the Node.
        """
        self.data = val
        self.next = None


class Solution:
    def removeLoop(self, head):
        """
        Function to remove a loop in the linked list.

        Args:
            head: The head node of the linked list.

        Returns:
            None (Modifies the linked list in-place).

        Notes:
            This function removes the loop in the linked list without losing any nodes.
        """

        slow = head
        fast = head
        while fast is not None and fast.next is not None:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:  # Loop detected
                slow = head
                if slow == fast:  # Loop at the head node
                    while fast.next != slow:
                        fast = fast.next
                else:  # Loop somewhere other than the head node
                    while slow.next != fast.next:
                        slow = slow.next
                        fast = fast.next
                fast.next = None  # Remove the loop
        return
```

**Time Complexity**
- The time complexity of the removeLoop function is O(n), where n is the number of nodes in the linked list. The function uses Floyd's cycle-finding algorithm to detect and remove the loop. In the worst case, the algorithm traverses the linked list twice.

**Space Complexity**
- The space complexity of the code is O(1) because it uses only a constant amount of extra space, regardless of the size of the linked list.

# C++ Code
```cpp
//Linked list structure
struct Node {
    int data;
    Node* next;
    
    Node(int val) {
        data = val;
        next = NULL;
    }
};

class Solution {
public:
    /**
     * Function to remove a loop in the linked list.
     * @param head The head of the linked list.
     */
    void removeLoop(Node* head) {
        // Code to remove the loop without losing any nodes
    
        Node* slow = head;
        Node* fast = head;
        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {  // Loop detected
                slow = head;
                if (slow == fast) {  // Loop at the head node
                    while (fast->next != slow) {
                        fast = fast->next;
                    }
                } else {  // Loop somewhere other than the head node
                    while (slow->next != fast->next) {
                        slow = slow->next;
                        fast = fast->next;
                    }
                }
                fast->next = NULL;  // Remove the loop
            }
        }
        return;
    }
};
```
