# 491. Increasing Subsequences

## Description

Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2 .

**Example:**

```
Input: [4, 6, 7, 7]
Output: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
```

**Note:**

1. The length of the given array will not exceed 15.
2. The range of integer in the given array is [-100,100].
3. The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.

 

## Solution

```java
class Solution {
    public List<List<Integer>> findSubsequences(int[] nums) {
        List<List<Integer>> res = new LinkedList<>();
        backtrack(res, new LinkedList<>(), nums, 0);
        return res;
    }
    
    public void backtrack(List<List<Integer>> res, LinkedList<Integer> temp, int[] nums, int start) {
        if(temp.size() >= 2) res.add(new LinkedList<>(temp));
        HashSet<Integer> set = new HashSet<>();
        for(int i = start; i < nums.length; i++) {
            if(set.contains(nums[i])) continue;
            if(temp.isEmpty() || nums[i] >= temp.getLast()) {
                temp.add(nums[i]);
                backtrack(res, temp, nums, i + 1);
                temp.removeLast();
                set.add(nums[i]);
            }
            
        }
    }
}
```

