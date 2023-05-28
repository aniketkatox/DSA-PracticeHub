# Python code

```python 


import sys
sys.setrecursionlimit(10**9)

class Solution:
    """
    This class contains a method to reverse the order of all nodes at even positions in a given linked list.
    """
    
    def solve(self, A):
        """
        Reverses the order of nodes at even positions in the linked list.
        
        Parameters:
            A (ListNode): The head of the linked list.
        
        Returns:
            ListNode: The head of the modified linked list.
        """
        
        if not A or not A.next:
            return A
            
        odd_list_head = p1 = A
        even_list_head = p2 = A.next
        
        # Traverse the linked list to separate odd and even position nodes
        while p1.next and p2.next:
            p1.next = p1.next.next
            p1 = p1.next
            p2.next = p2.next.next
            p2 = p2.next
        
        if p1:
            p1.next = None
        if p2:
            p2.next = None
        
        # Reverse the even position nodes
        reversed_even_head = self.reverse(even_list_head)
        
        p1 = odd_list_head
        p2 = reversed_even_head
        
        # Merge the odd position nodes and reversed even position nodes
        while p1 and p2:
            temp1 = p1.next
            temp2 = p2.next
            
            p1.next = p2
            p2.next = temp1
            
            p1 = temp1
            p2 = temp2
        
        return odd_list_head
    
    
    def reverse(self, head):
        """
        Reverses the given linked list iteratively.
        
        Parameters:
            head (ListNode): The head of the linked list.
        
        Returns:
            ListNode: The head of the reversed linked list.
        """
        
        prev = None
        curr = head
        
        while curr:
            next_node = curr.next
            curr.next = prev
            prev = curr
            curr = next_node
        
        return prev



```

**Time Complexity**
- The time complexity of the solve function is O(N), where N is the number of nodes in the linked list. This is because we traverse the linked list once to separate the odd-indexed and even-indexed nodes, reverse the even-indexed nodes, and then merge the two lists back together. Each of these operations takes O(N) time.

**Space Complexity**
- The space complexity of the solve function is O(1) because we are performing the rearrangement in-place, without using any additional data structures that depend on the size of the input.
