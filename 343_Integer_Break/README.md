# 343. Integer Break

## Description

 Given a positive integer *n*, break it into the sum of **at least** two positive integers and maximize the product of those integers. Return the maximum product you can get.

**Example 1:**

```
Input: 2
Output: 1
Explanation: 2 = 1 + 1, 1 × 1 = 1.
```

**Example 2:**

```
Input: 10
Output: 36
Explanation: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36.
```

**Note**: You may assume that *n* is not less than 2 and not larger than 58.

## Description

```java
class Solution {
    public int integerBreak(int n) {
        int[] dp = new int[n + 1];
        for (int i = 1; i < n + 1; i++) {
            if (i == 1) dp[1] = 1;
            else if (i == 2) dp[2] = 2;
            else if (i == 3) dp[3] = 3;
            else {
                int lo = 1, hi = i - 1;
                while (lo <= hi) {
                    dp[i] = Math.max(dp[lo++] * dp[hi--], dp[i]);
                }
            }
        }
        
        if (n == 1) return 0;
        else if (n == 2) return 1;
        else if (n == 3) return 2;
        else return dp[n];
    }
}
```

