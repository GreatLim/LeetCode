# 47. Permutations II

## Description
Given a collection of **distinct** integers, return all possible permutations.

**Example:**

```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

## Solution

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> list = new LinkedList<List<Integer>>();
        List<Integer> tempList =  new LinkedList();
        backtrack(list, tempList, nums);
        return list;
        
    }
    
    public void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums) {
        if(tempList.size() == nums.length)  {
            list.add(new LinkedList(tempList));
            return;
        }
        for(int i = 0; i < nums.length; i++) {
            if(tempList.contains(nums[i])) continue;
            tempList.add(nums[i]);
            backtrack(list, tempList, nums);
            tempList.remove(tempList.size() - 1);
        }
    }
}
```
