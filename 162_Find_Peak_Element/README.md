# 162. Find Peak Element

##  Description

A peak element is an element that is greater than its neighbors.

Given an input array `nums`, where `nums[i] ≠ nums[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `nums[-1] = nums[n] = -∞`.

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2:**

```
Input: nums = [1,2,1,3,5,6,4]
Output: 1 or 5 
Explanation: Your function can return either index number 1 where the peak element is 2, 
             or index number 5 where the peak element is 6.
```

## Solution

### O(lgn) Solution

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int lo = 0;
        int hi = nums.length - 1;
        while(lo < hi) {
            int mid1 = (lo + hi) / 2;
            System.out.println(mid1);
            int mid2 = mid1 + 1;
            if(nums[mid2] > nums[mid1]) lo = mid2;
            else hi = mid1;
        }
        return lo;
    }
}
```

### O(n) Solution

```java
class Solution {
    public int findPeakElement(int[] nums) {
        for(int i = 1; i < nums.length; i++) {
            if(nums[i - 1] > nums[i]) return i - 1;
        }
        return nums.length - 1;
    }
}
```

