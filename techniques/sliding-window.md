# Sliding Window

Maintain a window [l, r] over the array, expand r and shrink l based on a
condition — avoids recomputation for every subarray.

    int slidingWindowMaxSum(vector<int> &a, int k) {
        int sum = 0, best = 0;
        for (int r = 0; r < a.size(); r++) {
            sum += a[r];
            if (r >= k) sum -= a[r - k];   // shrink from left once window > k
            if (r >= k - 1) best = max(best, sum);
        }
        return best;
    }

## Variable-size window (condition-based shrink)

    int longestSubarrayWithSumLEQ(vector<int> &a, int limit) {
        int l = 0, sum = 0, best = 0;
        for (int r = 0; r < a.size(); r++) {
            sum += a[r];
            while (sum > limit) {
                sum -= a[l];
                l++;
            }
            best = max(best, r - l + 1);
        }
        return best;
    }

Time complexity: O(n) — each pointer moves forward at most n times total
N limit: n up to ~1e7-1e8
