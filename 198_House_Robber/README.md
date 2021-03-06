# 198. House Robber

##  Description

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```



## Solution

### DP - Space O(1)

```java
class Solution {
    public int rob(int[] nums) {
        int curYes = 0, curNo = 0;
        for(int num : nums) {
            int preYes = curYes, preNo = curNo;
            curYes = preNo + num;
            curNo = Math.max(preYes, preNo);
        }
        return Math.max(curYes, curNo);
    }
}
```



### DP - Space O(n)

```java
class Solution {
    public int rob(int[] nums) {
        int[][] dp = new int[2][nums.length + 1];
        for(int i = 1; i <= nums.length; i++) {
            dp[0][i] = dp[1][i - 1] + nums[i - 1];
            dp[1][i] = Math.max(dp[0][i - 1], dp[1][i - 1]);
        }
        return Math.max(dp[0][nums.length], dp[1][nums.length]);
    }
}
```


