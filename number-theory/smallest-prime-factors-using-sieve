# Smallest Prime Factor (SPF) using Sieve

Precompute once, then factorize any number up to MAXN in O(log n).

    const int MAXN = 1e7;
    int spf[MAXN+1];

    void computeSPF() {
        for (int i = 2; i <= MAXN; i++) {
            if (spf[i] == 0) {
                for (int j = i; j <= MAXN; j += i)
                    if (spf[j] == 0) spf[j] = i;
            }
        }
    }

    vector<pair<int,int>> factorizeSPF(int n) {
        vector<pair<int,int>> res;
        while (n > 1) {
            int p = spf[n], cnt = 0;
            while (n % p == 0) { n /= p; cnt++; }
            res.push_back({p, cnt});
        }
        return res;
    }

Time complexity: O(N log log N) precompute, O(log n) per query
N limit: MAXN up to ~1e7 (memory-bound, needs int array)
