# Divisors of n (i*i method)

    vector<int> divisors(int n) {
        vector<int> res;
        for (int i = 1; (long long)i*i <= n; i++) {
            if (n % i == 0) {
                res.push_back(i);
                if (i != n/i) res.push_back(n/i);
            }
        }
        return res;
    }

Time complexity: O(sqrt(n))
N limit: works fine up to n ~ 1e12 within TL (sqrt(1e12) = 1e6 ops)
