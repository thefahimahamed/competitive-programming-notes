# Sum of Divisors

If n = p1^q1 * p2^q2 * ... * pk^qk,

    long long divisorSum(vector<pair<int,int>> &factors) {
        long long sum = 1;
        for (auto &f : factors) {
            long long p = f.first, q = f.second;
            long long term = 0, pw = 1;
            for (int i = 0; i <= q; i++) { term += pw; pw *= p; }
            sum *= term;
        }
        return sum;
    }

Time complexity: O(sqrt(n)) factorization + O(sum of qi) for products (small)
N limit: n up to ~1e12 (use long long / mod if sum overflows)
