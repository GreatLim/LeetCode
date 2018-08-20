# 312. Burst Balloons

## Description

Given `n` balloons, indexed from `0` to `n-1`. Each balloon is painted with a number on it represented by array `nums`. You are asked to burst all the balloons. If the you burst balloon `i` you will get `nums[left] * nums[i] * nums[right]` coins. Here `left` and `right`are adjacent indices of `i`. After the burst, the `left` and `right` then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

**Note:**

- You may imagine `nums[-1] = nums[n] = 1`. They are not real therefore you can not burst them.
- 0 ≤ `n` ≤ 500, 0 ≤ `nums[i]` ≤ 100

**Example:**

```
Input: [3,1,5,8]
Output: 167 
Explanation: nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
             coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
```

## Solution

```java
class Solution {
    public int maxCoins(int[] nums) {
        if(nums == null || nums.length == 0) return 0;
        int n = nums.length;
        int dp[][] = new int[n][n];
        for(int d = 0; d < n; d++) {
            for(int left = 0; left + d < n; left++) {
                int right = left + d;
                for(int i = left; i <= right; i++) {
                    int leftCoins = (left <= i - 1) ? dp[left][i - 1] : 0;
                    int rightCoins = (i + 1 <= right) ? dp[i + 1][right] : 0;
                    dp[left][right] = Math.max(get(nums, left - 1) * nums[i] * get(nums, right + 1) + leftCoins + rightCoins, dp[left][right]);
                }
            }
        }
        return dp[0][n - 1];
    }
    
    public int get(int[] nums, int i) {
        if(i < 0 || i >= nums.length) return 1;
        return nums[i];
    }
}
```

