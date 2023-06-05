# C++ Code

```cpp
class Solution {
public:
    /**
     * Calculates the length of the longest substring without repeating characters.
     * 
     * @param s The input string.
     * @return The length of the longest substring without repeating characters.
     *
     */
    int lengthOfLongestSubstring(string s) {
        map<char, int> mp; // Map to track character frequencies in the current window
        int n = s.length(); // Length of the input string
        int ans = 0; // Variable to store the length of the longest substring
        int i = 0, j = 0; // Pointers for the sliding window (i: left edge, j: right edge)

        while (j < n) {
            mp[s[j]]++; // Update the character frequency, potentially making the window invalid

            // When the window is invalid (duplicate characters), shrink the left edge until it becomes valid again
            while (mp[s[j]] > 1) {
                mp[s[i]]--;
                i++;
            }

            ans = max(ans, j - i + 1); // Store the length of the maximum window
            j++; // Expand the window by moving the right edge
        }

        return ans; // Return the length of the longest substring
    }
};
```

**Time Complexity**
- The time complexity of the lengthOfLongestSubstring function is O(n), where n is the length of the input string s. This is because the algorithm uses a sliding window approach and iterates through the string once, visiting each character exactly once.

**Space Complexity**
- The space complexity of the function is O(min(n, m)), where n is the length of the input string s and m is the size of the character set. The algorithm uses a map to track the frequency of characters in the current window. The space used by the map is bounded by the size of the character set or the length of the string, whichever is smaller.
