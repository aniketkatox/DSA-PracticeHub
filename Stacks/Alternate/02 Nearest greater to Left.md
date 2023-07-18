# C++ Code

```cpp
class Solution {
public:
    vector<int> NGL(vector<int> &v) {
        stack<int> st;
        vector<int> result(v.size(), -1);
        
        for(int i=0;i<v.size();i++){
            while(st.size() && st.top() <= v[i]){
                st.pop();
            }
            if(!st.empty()){
                result[i] =  st.top();
            }
            st.push(v[i]);
        }

        return result;
    }
};
```

**Time Complexity**
- O(N)

**Space Complexity**
- O(N)
