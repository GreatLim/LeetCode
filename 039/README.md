# 39. Combination Sum

## Description
Given a **set** of candidate numbers (`candidates`) **(without duplicates)** and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sums to `target`.

The **same** repeated number may be chosen from `candidates` unlimited number of times.

**Note:**

- All numbers (including `target`) will be positive integers.
- The solution set must not contain duplicate combinations.

**Example 1:**

```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```

**Example 2:**

```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

## Solution

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> list = new LinkedList<List<Integer>>();
        List<Integer> tempList = new LinkedList<Integer>();
        Arrays.sort(candidates);
        backTrace(list, tempList, candidates, target, 0);
        return list;
    }
    
    public void backTrace(List<List<Integer>> list, List<Integer> tempList,int[] nums, int remain, int start) {
        if(remain < 0) return;
        else if(remain == 0) {
            list.add(new ArrayList<>(tempList));
            return;
        }
        else {
            for(int i = start; i < nums.length; i++) {
                tempList.add(nums[i]);
                backTrace(list, tempList, nums, remain - nums[i], i);
                tempList.remove(tempList.size() - 1);
            }
        }
    }
}
```
