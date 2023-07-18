# C++ Code

```cpp
class Solution {
public:
    vector<int> NSR(vector<int> &v) {
        stack<int> st;
        vector<int> result(v.size(), -1);
        
        for(int i=0;i<v.size();i++){
            while(st.size() && v[st.top()] > v[i]){
                result[st.top()] = v[i];
                st.pop();
            }
            st.push(i);
        }

        return result;
    }
};
```

**Time Complexity**
- O(N)

**Space Complexity**
- O(N)
