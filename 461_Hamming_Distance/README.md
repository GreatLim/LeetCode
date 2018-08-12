# 461. Hamming Distance

## Description

The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.

Given two integers `x` and `y`, calculate the Hamming distance.

**Note:**
0 ≤ `x`, `y` < 231.

**Example:**

```
Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

The above arrows point to positions where the corresponding bits are different.
```

## Solution

```java
class Solution {
    public int hammingDistance(int x, int y) {
        int res = 0, n = x ^ y;
        while(n != 0) {
            res++;
            n &= n - 1;
        }
        return res;
    }
}
```

