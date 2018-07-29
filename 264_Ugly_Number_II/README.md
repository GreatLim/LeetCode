# 264. Ugly Number II

## Description

Write a program to find the `n`-th ugly number.

Ugly numbers are **positive numbers** whose prime factors only include `2, 3, 5`. 

**Example:**

```
Input: n = 10
Output: 12
Explanation: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.
```

**Note:**  

1. `1` is typically treated as an ugly number.
2. `n` **does not exceed 1690**.

## Solution

### DP

```java
class Solution {
    public int nthUglyNumber(int n) {
        int[] dp = new int[n];
        int p2 = 0, p3 = 0, p5 = 0;
        dp[0] = 1;
        for(int i = 1; i < n; i++) {
            dp[i] = Math.min(dp[p2] * 2, Math.min(dp[p3] * 3, dp[p5] * 5));
            if(dp[p2] * 2 == dp[i]) p2++;
            if(dp[p3] * 3 == dp[i]) p3++;
            if(dp[p5] * 5 == dp[i]) p5++;
        }
        return dp[n - 1];
    }
}
```

### First Try

```java
class Solution {
    public int nthUglyNumber(int n) {
        PriorityQueue<Long> pq = new PriorityQueue<Long>();
        pq.add((long) 1);
        for(int i = 0; i < n - 1; i++) {
            long temp = pq.poll();
            if(!pq.contains(temp * 2) && temp * 2 > 0) pq.add(temp * 2);
            if(!pq.contains(temp * 3) && temp * 3 > 0) pq.add(temp * 3);
            if(!pq.contains(temp * 5) && temp * 5 > 0) pq.add(temp * 5);
        }
        return pq.poll().intValue();
    }
}
```

 