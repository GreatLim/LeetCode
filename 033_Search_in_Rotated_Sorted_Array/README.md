# 33. Search in Rotated Sorted Array

## Description
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).

You are given a target value to search. If found in the array return its index, otherwise return `-1`.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

## Solution
```java
class Solution {
    public int search(int[] nums, int target) {
        int start = 0;
        int end = nums.length - 1;
        while(start <= end) {
            int mid = (start + end) / 2;
            if(target == nums[mid]) return mid;
            else if(target < nums[mid]) {
                if(target < nums[start] && nums[start] <= nums[mid]) start = mid + 1;
                else end = mid - 1;
            }
            else {
                if(target > nums[end] && nums[mid] <= nums[end]) end = mid - 1;
                else start = mid + 1;
            }
        }
        return -1;
    }
}
```
