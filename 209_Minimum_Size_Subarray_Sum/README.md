# 209. Minimum Size Subarray Sum

## Description

Given an array of **n** positive integers and a positive integer **s**, find the minimal length of a **contiguous** subarray of which the sum ≥ **s**. If there isn't one, return 0 instead.

**Example:** 

```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

**Follow up:**

If you have figured out the *O*(*n*) solution, try coding another solution of which the time complexity is *O*(*n* log *n*). 

## Solution


```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if(nums == null || nums.length == 0) return 0;
        int start = 0, end = 1;
        int len = Integer.MAX_VALUE, sum = nums[0];
        while (end <= nums.length) {
            if(sum < s) {
                if(end == nums.length) break;
                sum += nums[end];
                end ++;
            } else {
                len = Math.min(end - start, len);
                sum -= nums[start];
                start ++;
            }
        }
        return len == Integer.MAX_VALUE ? 0 : len;     
    }
}
```

### Concise Version

```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if(nums == null || nums.length == 0) return 0;
        int start = 0, end = 0;
        int len = Integer.MAX_VALUE, sum = 0;
        while (end < nums.length) {
            sum += nums[end++];
            while (sum >= s) {
                len = Math.min(end - start, len);
                sum -= nums[start++];
            }
        }
        return len == Integer.MAX_VALUE ? 0 : len;     
    }
}
```

