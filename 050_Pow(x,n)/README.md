# 50. Pow(x, n)

## Description

Implement [pow(*x*, *n*)](http://www.cplusplus.com/reference/valarray/pow/), which calculates *x* raised to the power *n* (xn).

**Example 1:**

```
Input: 2.00000, 10
Output: 1024.00000
```

**Example 2:**

```
Input: 2.10000, 3
Output: 9.26100
```

**Example 3:**

```
Input: 2.00000, -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
```

**Note:**

- -100.0 < *x* < 100.0
- *n* is a 32-bit signed integer, within the range [−231, 231 − 1]

## Solution

```java
class Solution {
    public double myPow(double x, int n) {
        if(n == 0) return 1;
        long absN = Math.abs((long) n);
        double res = 1.0;
        
        while(absN > 0) {
            if(absN % 2 == 1) res *= x;
            absN /= 2;
            x *= x;
        }
        return n > 0 ? res : 1 / res;
        
    }
}
```



## Note

I couldn't find a clear explanation for an interative Log(n) solution so here's mine. The basic idea is to decompose the exponent into powers of 2, so that you can keep dividing the problem in half. For example, lets say

N = 9 = 2^3 + 2^0 = 1001 in binary. Then:

x^9 = x^(2^3) * x^(2^0)

We can see that every time we encounter a 1 in the binary representation of N, we need to multiply the answer with x^(2^i) where **i** is the **ith** bit of the exponent. Thus, we can keep a running total of repeatedly squaring x - (x, x^2, x^4, x^8, etc) and multiply it by the answer when we see a 1.

To handle the case where N=INTEGER_MIN we use a long (64-bit) variable. Below is solution:

```java
public class Solution {
    public double MyPow(double x, int n) {
        double ans = 1;
        long absN = Math.Abs((long)n);
        while(absN > 0) {
            if((absN&1)==1) ans *= x;
            absN >>= 1;
            x *= x;
        }
        return n < 0 ?  1/ans : ans;
    }
}
```