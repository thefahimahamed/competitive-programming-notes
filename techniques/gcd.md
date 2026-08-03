# GCD (Greatest Common Divisor)

## Euclidean Algorithm (recursive)

    long long gcd(long long a, long long b) {
        if (b == 0) return a;
        return gcd(b, a % b);
    }

Math: gcd(a, b) = gcd(b, a % b), since any common divisor of a and b also
divides a % b. Base case: gcd(a, 0) = a.

## Iterative version (avoids recursion depth issues)

    long long gcd(long long a, long long b) {
        while (b) {
            a %= b;
            swap(a, b);
        }
        return a;
    }

## Built-in (C++)

    __gcd(a, b);   // works for int/long long, in <algorithm>
    std::gcd(a, b); // C++17, in <numeric>

## LCM using GCD

    long long lcm(long long a, long long b) {
        return (a / gcd(a, b)) * b;   // divide first to avoid overflow
    }
