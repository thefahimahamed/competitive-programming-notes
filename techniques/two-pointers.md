# Two Pointers

Two indices moving through a structure (usually a sorted array) based on
a condition, avoiding an O(n^2) nested loop.

    int twoPointerSum(vector<int> &a, int target) {
        int l = 0, r = a.size() - 1;
        while (l < r) {
            int sum = a[l] + a[r];
            if (sum == target) return true;
            else if (sum < target) l++;
            else r--;
        }
        return false;
    }

Time complexity: O(n)
N limit: n up to ~1e7-1e8 (single pass, cache-friendly)
