# XOR Properties

a ^ a = 0
a ^ 0 = a
a ^ b = b ^ a          (commutative)
(a ^ b) ^ c = a ^ (b ^ c)   (associative)

Key consequence: XOR-ing a number with itself cancels it out. This makes XOR
useful for finding a "unique" element among duplicates — pairs cancel,
the odd one out survives.

Example — find the single non-duplicate in an array where every other
element appears twice:

    int findUnique(vector<int> &arr) {
        int x = 0;
        for (int v : arr) x ^= v;
        return x;   // all paired values cancel to 0, only unique remains
    }

Time complexity: O(n)

# Prefix XOR and Range XOR Queries

Define prefix XOR: 
p0 = 0
p1 = a1
p2 = a1 ^ a2
...
pn = a1 ^ a2 ^ ... ^ an

To get XOR of a range [x, y] (1-indexed):

    range_xor(x, y) = p(y) ^ p(x-1)

Why it works: p(y) = a1^...^ay and p(x-1) = a1^...^a(x-1).
XOR-ing them cancels the common prefix a1^...^a(x-1), leaving only
a(x) ^ a(x+1) ^ ... ^ a(y) — exactly the range you want.

## Implementation

    vector<int> prefix(n+1);
    prefix[0] = 0;
    for (int i = 1; i <= n; i++)
        prefix[i] = prefix[i-1] ^ a[i];

    int rangeXOR(int x, int y) {
        return prefix[y] ^ prefix[x-1];
    }

Time complexity: O(n) to build prefix array, O(1) per range query
N limit: n up to ~1e7 comfortably (array size + build time)

# More Important Bitwise/XOR Properties

## AND / OR properties
a & a = a
a | a = a
a & 0 = 0
a | 0 = a
a & (all 1s) = a
a | (all 1s) = all 1s

## De Morgan's for bits
~(a & b) = ~a | ~b
~(a & b) = ~a | ~b

## n & -n → isolates the lowest set bit
    int lowestSetBit(int n) {
        return n & (-n);
    }
Math: -n in two's complement = ~n + 1. This flips everything below the lowest
set bit to 1s and the bit itself stays, so ANDing keeps only that one bit.
Example: n = 12 (1100), -n = ...110100, n & -n = 0100 (4)
Time complexity: O(1)

## a + b using bitwise (no + operator)
    int add(int a, int b) {
        while (b != 0) {
            int carry = a & b;
            a = a ^ b;
            b = carry << 1;
        }
        return a;
    }
Math: XOR gives sum without carry, AND gives carry positions, shift carry left and repeat until no carry remains.
Time complexity: O(log(max(a,b)))

## Sum of XOR of all pairs in an array
For each bit position, count how many numbers have that bit set (cnt) and
unset (n-cnt). That bit contributes cnt*(n-cnt) pairs where it's set in the
XOR, so contributes cnt*(n-cnt)*2^bit to total sum (multiply by 2 if counting
ordered pairs i≠j, or use as-is for i<j pairs — check problem's definition).

    long long sumXORPairs(vector<int> &a) {
        long long total = 0;
        int n = a.size();
        for (int bit = 0; bit < 30; bit++) {
            int cnt = 0;
            for (int x : a) if (x & (1 << bit)) cnt++;
            total += (long long)cnt * (n - cnt) * (1LL << bit);
        }
        return total;
    }
Time complexity: O(n log(max value))

## n XOR (n-1) → all bits from lowest set bit down become 1
Useful for isolating/masking below the lowest set bit.

## Check if two numbers have opposite signs
    bool oppositeSign(int a, int b) {
        return (a ^ b) < 0;
    }
Math: sign bit differs → XOR's sign bit is 1 → result negative.
Time complexity: O(1)

## XOR from 1 to n (closed form, no loop needed)
    int xorUpto(int n) {
        if (n % 4 == 0) return n;
        if (n % 4 == 1) return 1;
        if (n % 4 == 2) return n + 1;
        return 0; // n % 4 == 3
    }
Useful for computing prefix XOR p(y) or p(x-1) in O(1) instead of O(n) when
the array is just 1..n (or combined with actual array prefix XOR for general arrays).
Time complexity: O(1)
