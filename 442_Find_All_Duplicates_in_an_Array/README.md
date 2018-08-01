# 442. Find All Duplicates in an Array

## Description

Given an array of integers, 1 ≤ a[i] ≤ *n* (*n* = size of array), some elements appear **twice** and others appear **once**.

Find all the elements that appear **twice** in this array.

Could you do it without extra space and in O(*n*) runtime?

**Example:**

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```





## Solution

```java
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        LinkedList res = new LinkedList();
        for(int num : nums) {
            int index = Math.abs(num) - 1;
            if(nums[index] < 0) res.add(index + 1);
            else nums[index] = - nums[index];
        }
        return res;
    }
}
```

