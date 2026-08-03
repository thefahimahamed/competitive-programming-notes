# Prime Check using Sieve of Eratosthenes

    const int MAXN = 1e7;
    bool isComposite[MAXN+1];

    void sieve() {
        isComposite[0] = isComposite[1] = true;
        for (int i = 2; (long long)i*i <= MAXN; i++) {
            if (!isComposite[i]) {
                for (int j = i*i; j <= MAXN; j += i)
                    isComposite[j] = true;
            }
        }
    }
    // isComposite[x] == false → x is prime

Time complexity: O(N log log N)
N limit: MAXN up to ~1e7-1e8 practical (memory-bound, 1e7 booleans ≈ 10MB)
