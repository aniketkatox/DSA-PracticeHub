**Time Complexity**
- The time complexity for both the get and put operations is constant time, making the implementation efficient for large caches.

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
