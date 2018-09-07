# 862. Shortest Subarray with Sum at Least K

## Description

Return the **length** of the shortest, non-empty, contiguous subarray of `A` with sum at least `K`.

If there is no non-empty subarray with sum at least `K`, return `-1`.

 


**Example 1:**

```
Input: A = [1], K = 1
Output: 1
```

**Example 2:**

```
Input: A = [1,2], K = 4
Output: -1
```

**Example 3:**

```
Input: A = [2,-1,2], K = 3
Output: 3
```

 

**Note:**

1. `1 <= A.length <= 50000`
2. `-10 ^ 5 <= A[i] <= 10 ^ 5`
3. `1 <= K <= 10 ^ 9`

 

## Solution

```java
class Solution {
    public int shortestSubarray(int[] A, int K) {
        int n = A.length, res = Integer.MAX_VALUE;
        int[] dp = new int[n + 1];
        for (int i = 1; i < n + 1; i++) 
            dp[i] = A[i - 1] + dp[i - 1];
        Deque<Integer> q = new LinkedList<>();
        for (int i = 0; i < n + 1; i++) {
            while (q.size() > 0 && dp[i] - dp[q.peekFirst()] >= K) 
                res = Math.min(res, i - q.pollFirst());
            while (q.size() > 0 && dp[i] <= dp[q.peekLast()])
                q.pollLast();
            q.offerLast(i);
        }
        return (res == Integer.MAX_VALUE) ? -1 : res;
    }
}
```

