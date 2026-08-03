# Kth Term via Difference Sequences

If a sequence's k-th finite difference is constant, the sequence follows a
degree-k polynomial in n. Take differences repeatedly until they become
constant — the number of steps taken tells you the polynomial degree.

## 1st difference constant → linear sequence

    a(n) = a*n + d

Example: 3, 7, 11, 15, ...
Diff: 4, 4, 4 (constant at step 1) → degree 1
a = common difference = 4
d = a(1) - a = 3 - 4 = -1
a(n) = 4n - 1

## 2nd difference constant → quadratic sequence

    a(n) = a*n^2 + b*n + d

Example: 2, 6, 12, 20, 30, ...
1st diff: 4, 6, 8, 10
2nd diff: 2, 2, 2 (constant at step 2) → degree 2
a = (2nd diff)/2 = 2/2 = 1
Solve using 3 known points (n=1,2,3) to get b and d:
a(1)=2 → a+b+d=2
a(2)=6 → 4a+2b+d=6
=> b=2, d=-1
a(n) = n^2 + 2n - 1

## 3rd difference constant → cubic sequence

    a(n) = a*n^3 + b*n^2 + c*n + d

Take differences 3 times until constant. Solve for a,b,c,d using 4 known
terms (n=1,2,3,4) via simultaneous equations.

## 4th difference constant → quartic

    a(n) = a*n^4 + b*n^3 + c*n^2 + d*n + e

Same idea — 4 difference steps to reach constant, solve using 5 known terms.

## General trick (any k-th degree)

1. Write out the sequence, take differences repeatedly.
2. Count how many diff-steps it takes to become constant → that's the degree k.
3. Leading coefficient = (constant value at step k) / k!
4. Plug in first k+1 terms of the sequence into a(n) = a*n^k + b*n^(k-1) + ... 
   and solve the resulting linear system for remaining coefficients.
5. Shortcut for competitive programming: if you just need a(n) for large n
   and know it's polynomial of degree k, use Lagrange interpolation on the
   first (k+1) known points instead of solving by hand — much faster to code.

Time complexity: O(k) to find degree, O(k^2) to solve coefficients (or O(k^2) via Lagrange interpolation)
N limit: works for any k, but manual coefficient-solving gets messy past k=3; use Lagrange interpolation for k ≥ 4 in code
