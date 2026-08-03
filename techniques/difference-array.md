# Difference Array

Used for range-update, point-query problems — apply k range updates in
O(k), then compute final array in one O(n) pass.

    vector<int> diff(n+1, 0);
    void rangeUpdate(int l, int r, int val) {
        diff[l] += val;
        diff[r+1] -= val;
    }
    // after all updates:
    vector<int> result(n);
    result[0] = diff[0];
    for (int i = 1; i < n; i++) result[i] = result[i-1] + diff[i];

Time complexity: O(1) per update, O(n) to build final array
N limit: n up to ~1e7-1e8
