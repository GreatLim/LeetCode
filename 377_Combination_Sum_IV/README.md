# 377. Combination Sum IV

## Description

Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

**Example:**

```
nums = [1, 2, 3]
target = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 7.
```

**Follow up:**
What if negative numbers are allowed in the given array?
How does it change the problem?
What limitation we need to add to the question to allow negative numbers?

**Credits:**
Special thanks to [@pbrother](https://leetcode.com/pbrother/) for adding this problem and creating all test cases.



## Solution

### Iterative Version

```java
class Solution {
    
    public int combinationSum4(int[] nums, int target) {
        int[] dp = new int[target + 1];
        dp[0] = 1;
        for(int i = 1; i < target + 1; i++) {
            for(int j = 0; j < nums.length; j++) {
                if(i - nums[j] >= 0) dp[i] += dp[i - nums[j]];
            }
        }
        return dp[target];
        
    }
}
```

### Recursion Version

```java
class Solution {
    public int[] dp;
    
    public int combinationSum4(int[] nums, int target) {
        dp = new int[target + 1];
        Arrays.fill(dp, -1);
        helper(nums, target);
        return dp[target];
    }
    
    public int helper(int[] nums, int target) {
        if(target == 0) return 1;
        if(dp[target] != -1) return dp[target];
        int res = 0;
        for(int i = 0; i < nums.length; i++) {
            if(target - nums[i] >= 0) 
                res += helper(nums, target - nums[i]);
        }
        dp[target] = res;
        return res;
    }
}
```

