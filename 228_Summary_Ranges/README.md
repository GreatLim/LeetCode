# 228. Summary Ranges

## Description

Given a sorted integer array without duplicates, return the summary of its ranges.

**Example 1:**

```
Input:  [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
Explanation: 0,1,2 form a continuous range; 4,5 form a continuous range.
```

**Example 2:**

```
Input:  [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
Explanation: 2,3,4 form a continuous range; 8,9 form a continuous range.
```

## Solution

```java
class Solution {
    public List<String> summaryRanges(int[] nums) {
        int start = 0;
        List<String> res = new LinkedList<String>();
        for (int i = 0; i < nums.length; i++) {
            if(i >= 1 && nums[i] != nums[i - 1] + 1) {
                int end = i - 1;
                String s;
                if(end == start) s = String.valueOf(nums[start]);
                else s = nums[start] + "->" + nums[end];
                res.add(s);
                start = i;
            } 
            if(i == nums.length - 1) {
                int end = i;
                String s;
                if(end == start) s = String.valueOf(nums[start]);
                else s = nums[start] + "->" + nums[end];
                res.add(s);
                start = i;
            }
        }
        return res;
    }
}
```



