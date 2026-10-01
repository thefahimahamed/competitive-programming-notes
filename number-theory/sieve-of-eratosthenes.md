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

    // bitset odd sieve
    const int mx = 1e8 + 9; //max value of n
    const int mxprm = 6e6 + 9; //max number of primes

    int psz = 0; //keeping count the number of primes discovered
    bitset <mx> mark; //to keep track of primes
    uint primes[mxprm]; //to store the primes
    void sieve() 
    { //just a prime sieve code
    mark[0] = mark[1] = 1;
    primes[psz++] = 2;
    int lim = sqrt(mx * 1.0) + 2;
    for (int i = 4; i < mx; i += 2) mark[i] = 1;
    for (int i = 3; i < mx; i += 2) 
        {
        if (!mark[i]) 
            {
            primes[psz++] = i;
            if (i <= lim)
                for (int j = i * i; j < mx; j += i)
                    mark[j] = 1;
            }
        }
    }
Time complexity: O(N log log N)
N limit: MAXN up to ~1e7-1e8 practical (memory-bound, 1e7 booleans ≈ 10MB)
