# 15. 3Sum

[clike here](https://leetcode.com/problems/3sum/description/)

## Description
Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

##Solution
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new LinkedList<>();
        int i = 0;
        int left;
        int right = nums.length - 1;
        while(i < nums.length - 2 && nums[i] <= 0) {
            while(i < nums.length - 2 && i > 0 && nums[i - 1] == nums[i]) i++;
            if(i >= nums.length - 2) break;
            left = i + 1;
            int target = -nums[i];
            while(left < right) {
                int sum = nums[left] + nums[right];
                if(sum == target) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    do {
                    right--;
                    } while(right > 0 && nums[right] == nums[right + 1]);
                    do {
                    left++;
                    } while(left < nums.length && nums[left] == nums[left - 1]);
                }
                else if(sum < target) left++;
                else if(sum > target) right--;
            }
            i++;
            right = nums.length - 1;
        }
        return result;
    }
}
```

## Note

* Arrays.sort()
* List<List<Integer>>
* LinkedList & ArrayList

## Todo

* make solution more concise