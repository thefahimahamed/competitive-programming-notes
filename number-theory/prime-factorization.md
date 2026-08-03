# Prime Factorization

n = p1^q1 * p2^q2 * p3^q3 * ...

## Basic O(sqrt(n)) factorization

    vector<pair<int,int>> primeFactors(int n) {
        vector<pair<int,int>> res;
        for (int p = 2; (long long)p*p <= n; p++) {
            if (n % p == 0) {
                int cnt = 0;
                while (n % p == 0) { n /= p; cnt++; }
                res.push_back({p, cnt});
            }
        }
        if (n > 1) res.push_back({n, 1}); // remaining prime factor
        return res;
    }

Time complexity: O(sqrt(n)) per number
N limit: n up to ~1e12 per call is fine
