# Prefix Sum / Suffix Sum

    vector<long long> prefixSum(vector<int> &a) {
        int n = a.size();
        vector<long long> pre(n+1, 0);
        for (int i = 0; i < n; i++) pre[i+1] = pre[i] + a[i];
        return pre;
    }
    // range sum [l, r] (0-indexed, inclusive) = pre[r+1] - pre[l]

Time complexity: O(n) build, O(1) per range query
N limit: n up to ~1e7-1e8
