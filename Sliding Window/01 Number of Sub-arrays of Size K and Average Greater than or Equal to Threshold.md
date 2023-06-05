# C++ Code

```cpp

class Solution {
public:
    int numOfSubarrays(vector<int>& arr, int k, int threshold) {
        int count = 0; // Variable to keep track of the count of subarrays
        int sum = 0; // Variable to store the accumulative sum
        int t = k * threshold; // Minimum sum for subarrays of length K (sliding window)

        for (int i = 0; i < arr.size(); i++) {
            sum += arr[i]; // Add the current element to the accumulative sum (add head)

            if (i < k - 1) {
                continue; // Wait until the sliding window reaches the threshold size
            }

            if (i >= k) {
                sum -= arr[i - k]; // Subtract the element at the tail from the accumulative sum
            }

            if (sum >= t) { // Check if the sum meets the threshold
                count++; // Increment the count of valid subarrays
            }
        }
        return count; // Return the total count of subarrays
    }
};


```
**Time Complexity**
-The time complexity is O(n), where n is the size of array.

**Space Complexity**
-The space complexity is O(1) because we are only using a constant amount of additional space.
