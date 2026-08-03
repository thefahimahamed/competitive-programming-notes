# Binary Search (on array / on answer)

## Standard binary search (find value in sorted array)

    int binarySearch(vector<int> &a, int target) {
        int lo = 0, hi = a.size() - 1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (a[mid] == target) return mid;
            else if (a[mid] < target) lo = mid + 1;
            else hi = mid - 1;
        }
        return -1;
    }

## Binary search on answer (monotonic predicate)

Used when direct search isn't over an array, but over possible answer values
where a condition is monotonic (true...true...false...false or vice versa).

    int binarySearchOnAnswer(int lo, int hi, function<bool(int)> canDo) {
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (canDo(mid)) hi = mid;      // shrink toward smallest valid answer
            else lo = mid + 1;
        }
        return lo;
    }

Trick to identify binary search on answer: if increasing/decreasing a
candidate answer flips a yes/no condition exactly once, binary search
applies — don't need an actual array.

Time complexity: O(log n) per search, O(n log n) if used with a per-check O(n) validation loop
N limit: n up to ~1e18 for value-range binary search (log2(1e18) ≈ 60 iterations)
