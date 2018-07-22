# 215. Kth Largest Element in an Array

## Description

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

**Example 1:**

```
Input: [3,2,1,5,6,4] and k = 2
Output: 5
```

**Example 2:**

```
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
```

**Note:** 
You may assume k is always valid, 1 ≤ k ≤ array's length.

## Solution

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int i = nums.length - k;
        return findKthLargest(nums, i, 0, nums.length - 1);
    }
    
    private int findKthLargest(int[] nums, int k, int lo, int hi) {
        int i;
        if(lo >= hi) i = lo;
        else i = patition(nums, lo, hi);
        if(i == k) return nums[i];
        else if(i < k) return findKthLargest(nums, k, i + 1, hi);
        else return findKthLargest(nums, k, lo, i - 1);
    }
        
    private int patition(int[] nums, int lo, int hi) {
        int i = lo;
        int j = hi + 1;
        while(true) {
            while(nums[++i] < nums[lo]) 
                if(i == hi) break;
            while(nums[--j] > nums[lo])
                if(j == lo) break;
            if(i >= j) break;
            exchange(nums, i, j);
        }
        exchange(nums, lo, j);
        return j;
        
    }
    
    private void exchange(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

