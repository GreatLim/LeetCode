# 34. Search for a Range

## Description
Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

If the target is not found in the array, return `[-1, -1]`.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

## Solution

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if(nums.length == 0) return new int[]{-1, -1};
        int[] res = binarySearch(nums, 0, nums.length - 1, target);
        if(res[0] == -1) return new int[]{-1, -1};
        int max = res[0];
        int min = res[0];
        int[] res1 = binarySearch(nums, res[1], res[0] - 1, target);
        int[] res2 = binarySearch(nums, res[0] + 1, res[2], target);
        do {
            if(res1[0] >= 0) min = res1[0];
            res1 = binarySearch(nums, res1[1], res1[0] - 1, target);
        } while(res1[0] != -1);
        do {
            if(res2[0] >= 0) max = res2[0];
            res2 = binarySearch(nums, res2[0] + 1, res2[2], target);
        } while(res2[0] != -1);
        return new int[]{min, max};
    }
    
    public int[] binarySearch(int[] nums, int start, int end, int target) {
        if(start < 0 || end > nums.length || start > end) return new int[]{-1, start, end};
        else {
            while(start <= end) {
                int[] res = new int[3];
                int mid = (start + end) / 2;
                if(target == nums[mid]){
                    return new int[]{mid, start, end};
                } 
                else if(target > nums[mid]) start = mid + 1;
                else end = mid - 1;
            }
        }
        return new int[]{-1, start, end};
    }
}
```

## Todo

* make the solution more concise