# 90. Subsets II

## Description
Given a collection of integers that might contain duplicates, **nums**, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

## Solution

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> list = new LinkedList<List<Integer>>();
        List<Integer> tempList =  new LinkedList();
        list.add(new LinkedList(tempList));
        backtrack(list, tempList, nums, 0);
        return list;
        
    }
    
    public void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, int start) {
        for(int i = start; i < nums.length; i++) {
            if(start < i && nums[i] == nums[i - 1]) continue;
            tempList.add(nums[i]);
            list.add(new LinkedList(tempList));
            backtrack(list, tempList, nums, i + 1);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

