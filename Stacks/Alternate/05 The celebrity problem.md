A celebrity is a person who is known to all but does not know anyone at a party. If you go to a party of N people, find if there is a celebrity in the party or not.

# C++ Code

```cpp
#include <bits/stdc++.h>
using namespace std;

bool knows(int a, int b, vector<vector<bool>>& matrix) {
    return matrix[a][b];
}

int findTheCelebrity(vector<vector<bool>>& matrix, int n) {
    // Our potential celebrity
    int Celeb;
    stack<int> st;

    // Push all the elements into the stack
    for (int i = 0; i < n; i++) {
        st.push(i);
    }

    // Find a potential celebrity
    while (st.size() > 1) {
        int x = st.top();
        st.pop();
        int y = st.top();
        st.pop();
        if (knows(x, y, matrix)) {
            st.push(y);
        } else {
            st.push(x);
        }
    }

    // Potential candidate?
    Celeb = st.top();
    st.pop();

    // Check if C is actually a celebrity or not
    for (int i = 0; i < n; i++) {
        // In case a person does not know 'C' or 'C' doesn't know any person, return -1
        if (i != Celeb) {
            if (knows(Celeb, i, matrix) || !knows(i, Celeb, matrix)) {
                return -1;
            }
        }
    }

    return Celeb;
}

// Driver Function
int main() {
    int n = 4;
    vector<vector<bool>> matrix = {{0, 0, 0, 1},
                                   {0, 0, 0, 1},
                                   {0, 0, 0, 1},
                                   {0, 0, 0, 0}};

    int result = findTheCelebrity(matrix, n);

    if (result != -1) {
        cout << "The celebrity is person " << result << endl;
    } else {
        cout << "No celebrity found in the group." << endl;
    }

    return 0;
}
```
**Time Complexity**
- O(N)

**Space Complexity**
- O(N)
