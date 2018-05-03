# 78. Subsets

## Description
Given a set of **distinct** integers, *nums*, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

## Solution

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> list = new LinkedList<List<Integer>>();
        List<Integer> tempList =  new LinkedList();
        list.add(new LinkedList(tempList));
        backtrack(list, tempList, nums, 0);
        return list;
        
    }
    
    public void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, int start) {
        for(int i = start; i < nums.length; i++) {
            tempList.add(nums[i]);
            list.add(new LinkedList(tempList));
            backtrack(list, tempList, nums, i + 1);
            tempList.remove(tempList.size() - 1);
        }
    }
    
}
```

