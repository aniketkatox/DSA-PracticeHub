# C++ Code

```cpp
class Solution {
public:
    /**
     * Finds the minimum length of a contiguous subarray in 'nums' that has a sum greater than or equal to 'target'.
     * 
     * @param target The target sum.
     * @param nums The input array of integers.
     * @return The minimum length of a subarray with a sum greater than or equal to 'target', or 0 if no such subarray exists.
     */
    int minSubArrayLen(int target, vector<int>& nums) {
        int n = nums.size();
        int i = 0; // Left pointer of the sliding window
        int j = 0; // Right pointer of the sliding window
        int ans = INT_MAX; // Variable to store the minimum length of the subarray

        while (j < n) {
            target -= nums[j]; // Update the state by subtracting the current element
            // If the window is valid, move the left pointer to make it invalid again
            while (target <= 0) {
                ans = min(ans, j - i + 1); // Update the minimum length
                target += nums[i]; // Add the element at the left pointer to the state
                i++; // Move the left pointer to the right
            }
            j++; // Move the right pointer to the right
        }
        
        return (ans == INT_MAX) ? 0 : ans; // Return the minimum length or 0 if no such subarray exists
    }
};


```

**Time Complexity**
- The time complexity of the minSubArrayLen function is O(n), where n is the size of the input array nums. This is because the algorithm uses a sliding window approach to iterate through the array once.

**Space Complexity**
- The space complexity of the function is O(1). The algorithm uses a constant amount of extra space to store variables and indices, regardless of the size of the input array.
