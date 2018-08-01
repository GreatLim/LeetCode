# 448. Find All Numbers Disappeared in an Array

## Description

Given an array of integers where 1 ≤ a[i] ≤ *n* (*n* = size of array), some elements appear twice and others appear once.

Find all the elements of [1, *n*] inclusive that do not appear in this array.

Could you do it without extra space and in O(*n*) runtime? You may assume the returned list does not count as extra space.

**Example:**

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

##  Solution

### Space O(1)

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        LinkedList res = new LinkedList();
        for(int num : nums) {
            int index = Math.abs(num) - 1;
            nums[index] = Math.min(-nums[index], nums[index]);
        }
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] > 0) res.add(i + 1);
        }
        return res;
    }
}
```



### Fast Version

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        LinkedList res = new LinkedList();
        boolean[] existed = new boolean[nums.length];
        for(int num : nums)
            existed[num - 1] = true;

        for(int i = 0; i < nums.length; i++) 
            if(existed[i] == false) res.add(i + 1);
        
        return res;
    }
}
```

