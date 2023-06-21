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
