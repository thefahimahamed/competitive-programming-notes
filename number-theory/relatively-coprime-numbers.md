# Relatively Coprime Numbers

Two numbers a and b are coprime (relatively prime) if gcd(a, b) == 1
(they share no common factor other than 1).

## Check if two numbers are coprime

    bool isCoprime(int a, int b) {
        return __gcd(a, b) == 1;
    }

Time complexity: O(log(min(a,b))) (Euclidean algorithm)
N limit: a, b up to ~1e18 (fits in long long, gcd is fast regardless of size)

# Count numbers coprime to n in [1, n] (Euler's Totient)

phi(n) = n * Π (1 - 1/p) for each distinct prime p dividing n

    int phi(int n) {
        int result = n;
        for (int p = 2; (long long)p*p <= n; p++) {
            if (n % p == 0) {
                while (n % p == 0) n /= p;
                result -= result / p;
            }
        }
        if (n > 1) result -= result / n;
        return result;
    }

Time complexity: O(sqrt(n)) per number
N limit: n up to ~1e12 for single query

# Euler's Totient for all numbers up to N (Sieve version)

    const int MAXN = 1e6;
    int phi[MAXN+1];

    void computePhiSieve() {
        for (int i = 0; i <= MAXN; i++) phi[i] = i;
        for (int i = 2; i <= MAXN; i++) {
            if (phi[i] == i) { // i is prime
                for (int j = i; j <= MAXN; j += i)
                    phi[j] -= phi[j] / i;
            }
        }
    }

Time complexity: O(N log log N)
N limit: MAXN up to ~1e7 (memory-bound, int array)

# Key Facts
1. gcd(a, b) = 1 → a and b are coprime
2. Consecutive integers (n, n+1) are always coprime
3. Two distinct primes are always coprime
4. phi(n) gives count of numbers in [1, n] coprime to n — useful in modular inverse (when mod is prime, a and mod are automatically coprime)
