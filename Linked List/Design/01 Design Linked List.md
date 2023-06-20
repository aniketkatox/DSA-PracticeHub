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
