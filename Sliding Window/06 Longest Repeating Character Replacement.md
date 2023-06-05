# C++ Code

```cpp
class Solution {
public:
    /**
     * Calculates the length of the longest substring after replacing at most k characters.
     * 
     * @param s The input string.
     * @param k The maximum number of characters that can be replaced.
     * @return The length of the longest substring after replacements.
     */
    int characterReplacement(string s, int k) {
        vector<int> count(26); // Array to track the count of each character (A to Z)
        int maxCount = 0; // Variable to store the maximum count of a character

        int i = 0; // Left pointer of the sliding window
        int j = 0; // Right pointer of the sliding window

        int result = 0; // Variable to store the length of the longest substring

        while (j < s.size()) {
            count[s[j] - 'A']++; // Update the count of the current character
            maxCount = max(maxCount, count[s[j] - 'A']); // Update the maximum count

            // If the number of replacements needed is greater than k, move the left pointer
            if ((j - i + 1) - maxCount > k) {
                count[s[i] - 'A']--; // Decrease the count of the character at the left pointer
                i++; // Move the left pointer to the right
            }

            result = max(result, j - i + 1); // Update the length of the longest substring
            j++; // Move the right pointer to the right
        }

        return result; // Return the length of the longest substring
    }
};
```

**Time Complexity**
- The time complexity of the characterReplacement function is O(n), where n is the length of the input string s. This is because the algorithm uses a sliding window approach and iterates through the string once, visiting each character exactly once.

**Space Complexity**
- The space complexity of the function is O(1). The algorithm uses a fixed-size vector of 26 elements to track the count of each character. The space used by the vector is constant and independent of the input size.
