```cpp 
class SegmentTree {
private:
    vector<long long> tree;
    vector<long long> arr;
    int n;

    void build(int idx, int l, int r) {
        if (l == r) {
            tree[idx] = arr[l];
            return;
        }

        int mid = (l + r) / 2;
        build(2 * idx + 1, l, mid);
        build(2 * idx + 2, mid + 1, r);
        tree[idx] = tree[2 * idx + 1] + tree[2 * idx + 2];
    }

    long long query(int idx, int l, int r, int ql, int qr) {
        if (ql > r || qr < l) return 0;
        if (ql <= l && r <= qr) return tree[idx];

        int mid = (l + r) / 2;
        long long leftRes = query(2 * idx + 1, l, mid, ql, qr);
        long long rightRes = query(2 * idx + 2, mid + 1, r, ql, qr);

        return leftRes + rightRes;
    }

    void update(int idx, int l, int r, int pos, long long val) {
        if (l == r) {
            arr[l] = val;
            tree[idx] = val;
            return;
        }

        int mid = (l + r) / 2;
        if (pos <= mid) update(2 * idx + 1, l, mid, pos, val);
        else update(2 * idx + 2, mid + 1, r, pos, val);
        
        tree[idx] = tree[2 * idx + 1] + tree[2 * idx + 2];
    }

public:
    SegmentTree(const vector<long long>& input) {
        arr = input;
        n = arr.size();
        tree.resize(4 * n);
        build(0, 0, n - 1);
    }

    long long getSum(int l, int r) {
        return query(0, 0, n - 1, l, r);
    }

    void setValue(int pos, long long val) {
        update(0, 0, n - 1, pos, val);
    }
};
```
