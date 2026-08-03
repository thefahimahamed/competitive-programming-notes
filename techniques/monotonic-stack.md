# Monotonic Stack

Maintain a stack where elements are kept in increasing/decreasing order,
popping elements that violate the order — used for "next greater/smaller
element" style problems.

    vector<int> nextGreaterElement(vector<int> &a) {
        int n = a.size();
        vector<int> res(n, -1);
        stack<int> st;  // stores indices
        for (int i = 0; i < n; i++) {
            while (!st.empty() && a[st.top()] < a[i]) {
                res[st.top()] = a[i];
                st.pop();
            }
            st.push(i);
        }
        return res;
    }

Time complexity: O(n) — each element pushed/popped at most once
N limit: n up to ~1e7-1e8
