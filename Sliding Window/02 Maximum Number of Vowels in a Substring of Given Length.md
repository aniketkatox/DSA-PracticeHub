# C++ Code

```cpp

class Solution {
public:
    int maxVowels(string s, int k) {
        int n = s.length();
        int count = 0; // Variable to keep track of the vowel count in the current window
        int ans = 0; // Variable to store the maximum vowel count

        for (int i = 0; i < n; i++) {
            if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i' || s[i] == 'o' || s[i] == 'u') {
                count++; // Increment the vowel count if the current character is a vowel
            }

            if (i < k - 1) {
                continue; // Wait until the sliding window reaches the threshold size
            }

            if (i >= k) {
                if (s[i - k] == 'a' || s[i - k] == 'e' || s[i - k] == 'i' || s[i - k] == 'o' || s[i - k] == 'u') {
                    count--; // Decrement the vowel count if the character at the tail of the window is a vowel
                }
            }
            ans = max(ans, count); // Update the maximum vowel count if necessary
        }
        return ans; // Return the maximum vowel count
    }
};

```

**Time Complexity**
- The time complexity is O(n), where n is the size of array.

**Space Complexity**
- The space complexity is O(1) because we are only using constant amount of additional space.
