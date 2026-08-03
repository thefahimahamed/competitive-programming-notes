# Number of Divisors

If n = p1^q1 * p2^q2 * ... * pk^qk,

divisor_count(n) = (q1+1) * (q2+1) * ... * (qk+1)

    long long divisorCount(vector<pair<int,int>> &factors) {
        long long cnt = 1;
        for (auto &f : factors) cnt *= (f.second + 1);
        return cnt;
    }

Time complexity: O(sqrt(n)) (from factorization) + O(k) for the product
N limit: n up to ~1e12
