# Bitwise Basics

Operators: & (AND), | (OR), ^ (XOR), ~ (NOT), << (left shift), >> (right shift)

Each operates bit-by-bit on the binary representation of numbers.
Time complexity: O(1) per operation (O(word size), constant for fixed int/long long)

# Bit Shifting

Left shift: a << k  =  a * 2^k   (shifts bits left, fills with 0)
Right shift: a >> k =  a / 2^k   (shifts bits right, integer division, floor)

    int a = 5;      // 101
    a << 1;         // 1010 = 10  (5*2)
    a >> 1;         // 10   = 2   (5/2, floor)

Time complexity: O(1)
N limit: shift amount k must be < bit-width of type (k < 32 for int, k < 64 for long long) — undefined behavior otherwise

# NOT (~)

Flips every bit: 0 -> 1 and 1 -> 0.
Math: ~a = -(a+1)   (two's complement representation)

    int a = 5;   // ...0101
    ~a;          // ...1010 = -6

Time complexity: O(1)

# Swap Two Variables (XOR trick)

Uses XOR self-inverse property: a ^ a = 0, a ^ 0 = a

    void swapXOR(int &a, int &b) {
        a ^= b;
        b ^= a;
        a ^= b;
    }

Time complexity: O(1)
Note: fails if a and b are the same memory location (becomes 0) — prefer std::swap in practice, this is mainly a bit-trick to know.

# Check ith Bit

    bool checkBit(int n, int i) {
        return (n >> i) & 1;
    }

Math: shift bit i to position 0, then mask with 1.
Time complexity: O(1)

# Set ith Bit

    int setBit(int n, int i) {
        return n | (1 << i);
    }

Math: OR-ing with a mask that has only bit i as 1 forces that bit to 1, leaves others unchanged.
Time complexity: O(1)

# Clear ith Bit

    int clearBit(int n, int i) {
        return n & ~(1 << i);
    }

Math: ~(1<<i) has every bit 1 except position i → AND forces bit i to 0, keeps rest.
Time complexity: O(1)

# Toggle ith Bit

    int toggleBit(int n, int i) {
        return n ^ (1 << i);
    }

Math: XOR with 1 flips that bit (0->1 or 1->0), XOR with 0 leaves other bits unchanged.
Time complexity: O(1)

# Remove the Lowest Set Bit

    int removeLastSetBit(int n) {
        return n & (n - 1);
    }

Math: n-1 flips all bits after (and including) the lowest set bit; AND with n clears that lowest set bit, keeps everything above it unchanged.
Example: n = 12 (1100), n-1 = 11 (1011), n&(n-1) = 1000 (8)

Time complexity: O(1)

# Check if a Number is Power of 2

    bool isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;
    }

Math: a power of 2 has exactly one set bit. n & (n-1) clears the lowest set bit — if the result is 0, there was only one set bit to begin with.

Time complexity: O(1)

# Count Number of Set Bits

## Manual loop
    int countSetBits(int n) {
        int cnt = 0;
        while (n) {
            n &= (n - 1);  // removes lowest set bit each time
            cnt++;
        }
        return cnt;
    }

## Built-in (faster, preferred in CP)
    __builtin_popcount(n);        // for int
    __builtin_popcountll(n);      // for long long

Time complexity: O(number of set bits) for manual, O(1)/hardware-instruction for builtin
