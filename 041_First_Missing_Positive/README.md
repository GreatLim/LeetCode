# 41. First Missing Positive

## Description
Given an unsorted integer array, find the smallest missing positive integer.

**Example 1:**

```
Input: [1,2,0]
Output: 3
```

**Example 2:**

```
Input: [3,4,-1,1]
Output: 2
```

**Example 3:**

```
Input: [7,8,9,11,12]
Output: 1
```

**Note:**

Your algorithm should run in *O*(*n*) time and uses constant extra space.

## Solution

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        boolean[] res = new boolean[nums.length];
        for(int i = 0; i <nums.length; i++) {
            if(nums[i] > 0 && nums[i] <= nums.length) res[nums[i] - 1] = true;
        }
        for(int i = 0; i <nums.length; i++) {
            if(res[i] == false) return i + 1;
        }
        return nums.length + 1;
    }
}
```
