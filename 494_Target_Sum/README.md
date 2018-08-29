# 494. Target Sum

## Description

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols `+` and `-`. For each integer, you should choose one from `+` and `-` as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

**Example 1:**

```
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```

**Note:**

1. The length of the given array is positive and will not exceed 20.
2. The sum of elements in the given array will not exceed 1000.
3. Your output answer is guaranteed to be fitted in a 32-bit integer.

## Solution

```java
class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        int n = nums.length, sum = 0;
        for (int num : nums)
            sum += num;
        if(S > sum || S < -sum) return 0;
        int[][] dp = new int[n + 1][2 * sum + 1];
        dp[0][sum] = 1;
        for (int i = 1; i < n + 1; i++) {
            for (int j = 0; j < 2 * sum + 1; j++) {
                dp[i][j] += (j - nums[i - 1] >= 0 ? dp[i - 1][j - nums[i - 1]] : 0)
                    + (j + nums[i - 1] < 2 * sum + 1 ? dp[i - 1][j + nums[i - 1]] : 0);
            }
        }
        
        return dp[n][S + sum];
    }
}
```

