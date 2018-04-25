# 47. Permutations II

## Description
Given a collection of numbers that might contain duplicates, return all possible unique permutations.

**Example:**

```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

## Solution

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> list = new LinkedList<List<Integer>>();
        List<Integer> tempList =  new LinkedList();
        boolean[] used = new boolean[nums.length];
        backtrack(list, tempList, nums, used);
        return list;
        
    }
    
    public void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, boolean[] used) {
        if(tempList.size() == nums.length)  {
            list.add(new LinkedList(tempList));
            return;
        }
        for(int i = 0; i < nums.length; i++) {
            if(used[i] || (i > 0 && nums[i] == nums[i - 1]) && !used[i - 1]) continue;
            tempList.add(nums[i]);
            used[i] = true;
            backtrack(list, tempList, nums, used);
            tempList.remove(tempList.size() - 1);
            used[i] = false;
        }
    }
}
```
