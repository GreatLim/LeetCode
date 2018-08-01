# 300. Longest Increasing Subsequence

## Description

Given an unsorted array of integers, find the length of longest increasing subsequence.

**Example:**

```
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
```

**Note:**

- There may be more than one LIS combination, it is only necessary for you to return the length.
- Your algorithm should run in O(*n2*) complexity.

**Follow up:** Could you improve it to O(*n* log *n*) time complexity?



## Solution

### Binary Search

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums.length == 0 || nums == null) return 0;
        int n = nums.length;
        int[] tails = new int[n];
        int size = 0;
        for(int num : nums) {
            int lo = 0, hi = size;
            while(lo < hi) {
                int mid = (lo + hi) / 2;
                if(num > tails[mid]) lo = mid + 1;
                else hi = mid;
            }
            if(lo == size) size++;
            tails[lo] = num;
        }
        return size;
    }
}
```

### O(N^2)

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums.length == 0 || nums == null) return 0;
        int n = nums.length;
        int[] dp = new int[n];
        int max = 0;
        for(int i = 0; i < n; i++) 
            dp[i] = 1;
        
        for(int i = 1; i < n; i++) {
            for(int j = 0; j < i; j++) {
                if(nums[j] < nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }
        
        for(int num : dp) {
            max = Math.max(max, num);
        }
        return max;
    }
}
```





### Note

`tails` is an array storing the smallest tail of all increasing subsequences with length `i+1` in `tails[i]`.
For example, say we have `nums = [4,5,6,3]`, then all the available increasing subsequences are:

```
len = 1   :      [4], [5], [6], [3]   => tails[0] = 3
len = 2   :      [4, 5], [5, 6]       => tails[1] = 5
len = 3   :      [4, 5, 6]            => tails[2] = 6
```

We can easily prove that tails is a increasing array. Therefore it is possible to do a binary search in tails array to find the one needs update.

Each time we only do one of the two:

```
(1) if x is larger than all tails, append it, increase the size by 1
(2) if tails[i-1] < x <= tails[i], update tails[i]
```

Doing so will maintain the tails invariant. The the final answer is just the size.

**Java**

```java
public int lengthOfLIS(int[] nums) {
    int[] tails = new int[nums.length];
    int size = 0;
    for (int x : nums) {
        int i = 0, j = size;
        while (i != j) {
            int m = (i + j) / 2;
            if (tails[m] < x)
                i = m + 1;
            else
                j = m;
        }
        tails[i] = x;
        if (i == size) ++size;
    }
    return size;
}
// Runtime: 2 ms
```

