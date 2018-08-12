# 69. Sqrt(x)

## Description

Implement `int sqrt(int x)`.

Compute and return the square root of *x*, where *x* is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

**Example 1:**

```
Input: 4
Output: 2
```

**Example 2:**

```
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
```

## Solution

### Newton Method

```java
class Solution {
    public int mySqrt(int x) {
        long r = x;
        while(r * r > x) {
            r = (r + x / r) / 2;
        }
        return (int) r;
    }
}
```

### Binary Search

```java
class Solution {
    public int mySqrt(int x) {
        long left = 0, right = x;
        while(left <= right) {
            long mid = (left + right) / 2;
            if(mid * mid > x) right = mid - 1;
            else if(mid * mid < x) left = mid + 1;
            else return (int) mid;
        }
        return (int) right;
    }
}
```

