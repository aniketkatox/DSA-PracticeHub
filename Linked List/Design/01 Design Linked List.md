# Python
```python
class Node:
    def __init__(self, value):
        """
        Node class to represent a node in the linked list.

        Args:
            value (int): The value to be stored in the node.
        """
        self.val = value
        self.prev = None
        self.next = None


class MyLinkedList:
    def __init__(self):
        """
        MyLinkedList class to implement a doubly linked list.
        """
        self.size = 0
        self.leftDummy = Node(0)
        self.rightDummy = Node(0)
        self.leftDummy.next = self.rightDummy
        self.rightDummy.prev = self.leftDummy

    def get(self, index):
        """
        Get the value at the specified index in the linked list.

        Args:
            index (int): The index of the element to get.

        Returns:
            int: The value at the specified index if it exists, otherwise -1.
        """
        if index >= self.size:
            return -1

        temp = self.leftDummy.next
        while index > 0:
            temp = temp.next
            index -= 1

        return temp.val

    def addAtHead(self, val):
        """
        Add a node with the given value at the beginning of the linked list.

        Args:
            val (int): The value to add at the head.
        """
        newHead = Node(val)
        nextFromLeftDummy = self.leftDummy.next

        newHead.next = nextFromLeftDummy
        newHead.prev = self.leftDummy
        self.leftDummy.next = newHead
        nextFromLeftDummy.prev = newHead
        self.size += 1

    def addAtTail(self, val):
        """
        Add a node with the given value at the end of the linked list.

        Args:
            val (int): The value to add at the tail.
        """
        newTail = Node(val)
        prevFromRightDummy = self.rightDummy.prev

        newTail.next = self.rightDummy
        newTail.prev = prevFromRightDummy
        self.rightDummy.prev = newTail
        prevFromRightDummy.next = newTail
        self.size += 1

    def addAtIndex(self, index, val):
        """
        Add a node with the given value at the specified index in the linked list.

        Args:
            index (int): The index at which to add the node.
            val (int): The value to add at the specified index.
        """
        if index > self.size:
            return

        if index == 0:
            self.addAtHead(val)
            return

        if index == self.size:
            self.addAtTail(val)
            return

        newNode = Node(val)
        temp = self.leftDummy

        while index > 0:
            temp = temp.next
            index -= 1

        currNext = temp.next
        newNode.next = currNext
        newNode.prev = temp
        temp.next = newNode
        currNext.prev = newNode
        self.size += 1

    def deleteAtIndex(self, index):
        """
        Delete the node at the specified index from the linked list.

        Args:
            index (int): The index of the node to delete.
        """
        if index >= self.size:
            return

        temp = self.leftDummy

        while index > 0:
            temp = temp.next
            index -= 1

        nextPtr = temp.next.next
        deleteNode = temp.next

        temp.next = nextPtr
        nextPtr.prev = temp

        del deleteNode
        self.size -= 1

```

**Time Complexity**
- Overall, the time complexity of the provided code is primarily dependent on the operations that involve traversing the linked list, which have a time complexity of O(index).

**Space Complexity**
- The space complexity of the MyLinkedList class is O(N), where N is the number of nodes in the linked list. This is because we are using additional memory to store the nodes and pointers.

# C++ Code
```cpp
// Doubly Linked List
class Node {
public:
    int val;
    Node* prev;
    Node* next;

    Node(int value) {
        val = value;
        prev = nullptr;
        next = nullptr;
    }
};

class MyLinkedList {
public:
    int size = 0;
    Node* leftDummy;
    Node* rightDummy;

    MyLinkedList() {
        leftDummy = new Node(0);
        rightDummy = new Node(0);
        leftDummy->next = rightDummy;
        rightDummy->prev = leftDummy;
    }

    /**
     * Get the value at the specified index in the linked list.
     *
     * @param index The index of the element to get.
     * @return The value at the specified index if it exists, otherwise -1.
     */
     //Time Complexity-> O(index)
    int get(int index) {
        if (index >= size) {
            return -1;
        }

        Node* temp = leftDummy->next;

        while (index > 0) {
            temp = temp->next;
            index--;
        }
        return temp->val;
    }

    /**
     * Add a node with the given value at the beginning of the linked list.
     *
     * @param val The value to add at the head.
     */
     //Time Complexity-> O(1)
    void addAtHead(int val) {
        Node* newHead = new Node(val);
        Node* nextFromLeftDummy = leftDummy->next;

        newHead->next = nextFromLeftDummy;
        newHead->prev = leftDummy;
        leftDummy->next = newHead;
        nextFromLeftDummy->prev = newHead;
        size++;
    }

    /**
     * Add a node with the given value at the end of the linked list.
     *
     * @param val The value to add at the tail.
     */
    //Time Complexity-> O(1)
    void addAtTail(int val) {
        Node* newTail = new Node(val);
        Node* prevFromRightDummy = rightDummy->prev;

        newTail->next = rightDummy;
        newTail->prev = prevFromRightDummy;
        rightDummy->prev = newTail;
        prevFromRightDummy->next = newTail;
        size++;
    }

    /**
     * Add a node with the given value at the specified index in the linked list.
     *
     * @param index The index at which to add the node.
     * @param val The value to add at the specified index.
     */
     //Time Complexity-> O(index)
    void addAtIndex(int index, int val) {
        if (index > size) {
            return;
        }

        if (index == 0) {
            addAtHead(val);
            return;
        }

        if (index == size) {
            addAtTail(val);
            return;
        }

        Node* newNode = new Node(val);
        Node* temp = leftDummy;

        while (index > 0) {
            temp = temp->next;
            index--;
        }
        Node* currNext = temp->next;

        newNode->next = currNext;
        newNode->prev = temp;
        temp->next = newNode;
        currNext->prev = newNode;
        size++;
    }

    /**
     * Delete the node at the specified index from the linked list.
     *
     * @param index The index of the node to delete.
     */
     //Time Complexity-> O(index)
    void deleteAtIndex(int index) {
        if (index >= size) {
            return;
        }

        Node* temp = leftDummy;

        while (index > 0) {
            temp = temp->next;
            index--;
        }
        Node* nextPtr = temp->next->next;
        Node* deleteNode = temp->next;

        temp->next = nextPtr;
        nextPtr->prev = temp;

        delete deleteNode;
        size--;
    }
};
```
