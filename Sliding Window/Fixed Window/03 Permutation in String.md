# C++ Code

```cpp

class Solution {
public:
    /**
     * Check if s1 is a permutation (substring) of s2.
     *
     * @param s1 The first string to check.
     * @param s2 The second string to check.
     * @return True if s1 is a permutation of s2, False otherwise.
     */
    bool checkInclusion(string s1, string s2) {
        int len1 = s1.length();
        int len2 = s2.length();

        if (len1 > len2) {
            return false; // s1 cannot be a permutation of s2 if it is longer
        }

        // Create a map to count characters in s1
        map<char, int> charCount;

        // Fill the map with the characters and their counts from s1
        for (int i = 0; i < len1; i++) {
            charCount[s1[i]]++;
        }

        // Sliding window approach to check for permutation
        int matches = 0;
        for (int i = 0; i < len2; i++) {
            // Check if the current character is in s1
            if (charCount[s2[i]] > 0) {
                matches++; // Increment the match count
            }
            charCount[s2[i]]--; // Decrement the count of the current character

            if (i < len1 - 1) {
                continue; // Wait until the sliding window reaches the threshold size
            }

            if (i >= len1) {
                // Check if the character at the tail of the window needs to be considered
                charCount[s2[i - len1]]++;
                if (charCount[s2[i - len1]] > 0) {
                    matches--; // Decrement the match count
                }
            }

            if (matches == len1) {
                return true; // s1 is a permutation of s2
            }
        }
        return false; // s1 is not a permutation of s2
    }
};

```

**Time Complexity**
- The time complexity of the checkInclusion function is O(n1 + n2), where n1 is the length of string s1 and n2 is the length of string s2. This is because the function iterates over both strings once, performing constant-time operations such as map lookups and updates.

**Space Complexity**
- The space complexity of the function is O(n1), where n1 is the length of string s1. This is because the function uses a map charCount to store the count of characters in s1, which can have at most n1 distinct characters. Therefore, the space required by the map is proportional to the length of s1.
