# Python
```python
class Node:
    def __init__(self, key, value):
        """
        Node class to represent a node in the doubly linked list.

        Args:
            key (int): The key of the node.
            value (int): The value associated with the key.
        """
        self.key = key
        self.value = value
        self.prev = None
        self.next = None


class LRUCache:
    def __init__(self, capacity):
        """
        LRUCache class to implement a least recently used (LRU) cache.

        Args:
            capacity (int): The capacity of the LRUCache.
        """
        self.capacity = capacity
        self.cache = {}  # Hash map to store key-node mappings
        self.left = Node(0, 0)  # Left sentinel node
        self.right = Node(0, 0)  # Right sentinel node
        self.left.next = self.right
        self.right.prev = self.left

    def remove(self, node):
        """
        Remove a node from the list.

        Args:
            node (Node): The node to be removed.
        """
        prev_node = node.prev
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node

    def insert(self, node):
        """
        Insert a node at the right end of the list.

        Args:
            node (Node): The node to be inserted.
        """
        prev_node = self.right.prev
        prev_node.next = node
        self.right.prev = node
        node.prev = prev_node
        node.next = self.right

    def get(self, key):
        """
        Get the value associated with the given key from the LRUCache.

        Args:
            key (int): The key of the value to retrieve.

        Returns:
            int: The value associated with the given key, or -1 if not found.
        """
        if key in self.cache:
            node = self.cache[key]
            self.remove(node)
            self.insert(node)
            return node.value
        return -1

    def put(self, key, value):
        """
        Put a key-value pair into the LRUCache.
        If the key already exists, update the value and adjust its position in the cache.
        If the capacity is exceeded, remove the least recently used item.

        Args:
            key (int): The key of the item to be inserted or updated.
            value (int): The value associated with the key.
        """
        if key in self.cache:
            node = self.cache[key]
            self.remove(node)
            del self.cache[key]

        node = Node(key, value)
        self.cache[key] = node
        self.insert(node)

        if len(self.cache) > self.capacity:
            lru = self.left.next
            self.remove(lru)
            del self.cache[lru.key]

```

**Time Complexity**
- The time complexity for both the get and put operations is constant time O(1), making the implementation efficient for large caches.

**Space Complexity**
- The space complexity of the LRUCache class is O(capacity) since it can store up to capacity key-value pairs in the hash map and linked list.

# C++ Code
```cpp
// Doubly Linked List Node
class Node {
public:
    int k;      // Key
    int val;    // Value
    Node* prev; // Pointer to the previous node
    Node* next; // Pointer to the next node

    // Node constructor
    Node(int key, int value) {
        k = key;
        val = value;
        prev = NULL;
        next = NULL;
    }
};

class LRUCache {
public:
    int cap;                          // Capacity of the LRUCache
    unordered_map<int, Node*> mp;     // Hash map to store key-node mappings
    Node* left;                       // Left sentinel node
    Node* right;                      // Right sentinel node

    // Remove a node from the list
    void remove(Node* node) {
        Node* prev_node = node->prev;
        Node* next_node = node->next;

        prev_node->next = next_node;
        next_node->prev = prev_node;
    }

    // Insert a node at the right end of the list
    void insert(Node* node) {
        Node* prev_node = right->prev;

        prev_node->next = node;
        right->prev = node;

        node->prev = prev_node;
        node->next = right;
    }

    // LRUCache constructor
    LRUCache(int capacity) {
        cap = capacity;

        left = new Node(0, 0);
        right = new Node(0, 0);

        left->next = right;
        right->prev = left;
    }
    
    /**
     * Get the value associated with the given key from the LRUCache.
     * @param key The key of the value to retrieve.
     * @return The value associated with the given key, or -1 if not found.
     */
    int get(int key) {
        if (mp.find(key) != mp.end()) {
            remove(mp[key]);
            insert(mp[key]);
            return mp[key]->val;
        }
        return -1;
    }
    
    /**
     * Put a key-value pair into the LRUCache.
     * If the key already exists, update the value and adjust its position in the cache.
     * If the capacity is exceeded, remove the least recently used item.
     * @param key The key of the item to be inserted or updated.
     * @param value The value associated with the key.
     */
    void put(int key, int value) {
        if (mp.find(key) != mp.end()) {
            remove(mp[key]);

            // Free allocated memory for the removed node
            delete mp[key];
        }
        mp[key] = new Node(key, value);
        insert(mp[key]);

        if (mp.size() > cap) {
            Node* lru = left->next;

            remove(lru);
            mp.erase(lru->k);

            // Free allocated memory for the removed node
            delete lru;
        }
    }
};
```
