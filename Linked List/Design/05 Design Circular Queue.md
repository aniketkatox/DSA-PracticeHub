# Python Code

```python
class Node:
    def __init__(self, value):
        self.val = value
        self.prev = None
        self.next = None

class MyCircularQueue:
    def __init__(self, k):
        self.space = k
        self.left = Node(0)
        self.right = Node(0)
        self.left.next = self.right
        self.right.prev = self.left
    
    def enQueue(self, value):
        if self.isFull():
            return False
        new_node = Node(value)
        new_node.prev = self.right.prev
        new_node.next = self.right
        self.right.prev.next = new_node
        self.right.prev = new_node
        self.space -= 1
        return True
    
    def deQueue(self):
        if self.isEmpty():
            return False
        self.left.next = self.left.next.next
        self.left.next.prev = self.left
        self.space += 1
        return True
    
    def Front(self):
        if self.isEmpty():
            return -1
        return self.left.next.val
    
    def Rear(self):
        if self.isEmpty():
            return -1
        return self.right.prev.val
    
    def isEmpty(self):
        return self.left.next == self.right
    
    def isFull(self):
        return self.space == 0

```

**Time Complexity**
- Overall, each operation has a time complexity of O(1), which means they execute in constant time.

**Space Complexity**
- The space complexity is O(k), where k is the given capacity of the circular queue. The space is used to store the nodes in the doubly linked list that represents the queue. In the worst case, the number of nodes stored in the queue would be equal to the capacity of the circular queue.

# C++ Code

```cpp
//Doubly linked list
class Node{
public:
    int val;
    Node* prev;
    Node* next;

    Node(int value){
        val = value;
        prev = NULL;
        next = NULL;
    }
};

class MyCircularQueue {
public:
    int space;
    Node* left;
    Node* right;

    MyCircularQueue(int k) {
        space = k;

        left = new Node(0);
        right = new Node(0);

        left->next = right;
        right->prev = left;
    }
    
    bool enQueue(int value) {
        if(isFull()){
            return false;
        }
        Node* newNode = new Node(value);
        right->prev->next = newNode;     
        newNode->prev = right->prev;
        right->prev = newNode;
        newNode->next = right;
        space--;

        return true;
    }
    
    bool deQueue() {
        if(isEmpty()){
            return false;
        }
        left->next = left->next->next;
        left->next->prev = left;
        space++;

        return true;
    }
    
    int Front() {
        if(isEmpty())   return-1;
        return left->next->val;
    }
    
    int Rear() {
        if(isEmpty())   return -1;
        return right->prev->val;
    }
    
    bool isEmpty() {
        if(left->next == right){
            return true;
        }
        return false;
    }
    
    bool isFull() {
        if(space == 0){
            return true;
        }
        return false;
    }
};
```
