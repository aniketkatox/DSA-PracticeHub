# Python
```python
from collections import defaultdict, OrderedDict

class LFUCache:
    def __init__(self, capacity):
        """
        LFUCache class to implement a least frequently used (LFU) cache.

        Args:
            capacity (int): The capacity of the LFUCache.
        """
        self.capacity = capacity
        self.lfu = 0  # Current least frequency used
        self.values = {}  # {key: (value, frequency)}
        self.keys = defaultdict(OrderedDict)  # {frequency: OrderedDict of keys}
        self.iters = {}  # {key: iterator}

    def update(self, key):
        """
        Update the frequency of a key and adjust its position in the frequency list.

        Args:
            key (int): The key to update.
        """
        freq = self.values[key][1]
        iter = self.iters[key]
        del self.keys[freq][key]  # Remove key from current frequency
        freq += 1
        self.keys[freq][key] = True  # Add key to new frequency
        self.values[key] = (self.values[key][0], freq)  # Update frequency in values
        self.iters[key] = next(reversed(self.keys[freq]))  # Update iterator

        if not self.keys[self.lfu]:  # If minimum frequency list becomes empty
            self.lfu += 1

    def get(self, key):
        """
        Get the value associated with the given key from the LFUCache.

        Args:
            key (int): The key of the value to retrieve.

        Returns:
            int: The value associated with the given key, or -1 if not found.
        """
        if key not in self.values:
            return -1
        self.update(key)
        return self.values[key][0]

    def put(self, key, value):
        """
        Put a key-value pair into the LFUCache.
        If the key already exists, update the value and increase its frequency.
        If the capacity is exceeded, evict the least frequently used item.

        Args:
            key (int): The key of the item to be inserted or updated.
            value (int): The value associated with the key.
        """
        if key in self.values:
            self.values[key] = (value, self.values[key][1])
            self.update(key)
            return

        if len(self.values) == self.capacity:
            evict = next(iter(self.keys[self.lfu]))  # Get the first key from the minimum frequency list
            del self.values[evict]
            del self.iters[evict]
            del self.keys[self.lfu][evict]

        self.lfu = 1
        self.values[key] = (value, self.lfu)
        self.keys[self.lfu][key] = True
        self.iters[key] = next(reversed(self.keys[self.lfu]))

```

**Time Complexity**
- The time complexity for both the get and put operations is constant time O(1), making the implementation efficient for large caches.

**Space Complexity**
- The space complexity of the LFUCache class is O(capacity) since it can store up to capacity key-value pairs in the hash map and maintain frequency lists for the keys.

# C++ Code
```cpp
class LFUCache {
public:
    int cap, lfu;                                   // Capacity and current least frequency used
    unordered_map<int, pair<int, int>> values;      // {key: {value, frequency}}
    unordered_map<int, list<int>> keys;            // {frequency: list of keys}
    unordered_map<int, list<int>::iterator> iters;  // {key: iterator}

    // Update the frequency of a key and adjust its position in the frequency list
    void update(int key) {
        int freq = values[key].second;
        auto iter = iters[key];
        keys[freq].erase(iter);   //iterator is useful here((1)removing node from list)
        freq++;
        keys[freq].push_back(key);    //(2)inserting node in list
        values[key].second = freq;  //update frequency in map too
        iters[key] = --keys[freq].end();  //iterator of this node

        if (keys[lfu].empty()) {  //if minimum frequency list gets empty
            lfu++;
        }
    }

    // LFUCache constructor
    LFUCache(int capacity) {
        cap = capacity;
        lfu = 0;
    }
    
    /**
     * Get the value associated with the given key from the LFUCache.
     * @param key The key of the value to retrieve.
     * @return The value associated with the given key, or -1 if not found.
     */
    int get(int key) {
        if (values.find(key) == values.end()) {
            return -1;
        }
        update(key);
        return values[key].first;
    }
    
    /**
     * Put a key-value pair into the LFUCache.
     * @param key The key of the item to be inserted or updated.
     * @param value The value associated with the key.
     */
    void put(int key, int value) {
          //If the key already exists, update the value and increase its frequency.
        if (values.find(key) != values.end()) {
            values[key].first = value;
            update(key);
            return;
        }
          //If the capacity is exceeded, evict the least frequently used item,
          //evict before adding new node otherwise lfu changes will result wrong answer.
        if (values.size() == cap) {
            int evict = keys[lfu].front();
            keys[lfu].pop_front();  //lfu is useful here
            values.erase(evict);
            iters.erase(evict);
        }

        lfu = 1;      //bcz this key occured first time
        values[key] = {value, 1};
        keys[1].push_back(key);
        iters[key] = --keys[1].end();
    }
};
```
