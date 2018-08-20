# 360. Sort Transformed Array

## Description

Given a **sorted** array of integers *nums* and integer values *a*, *b* and *c*. Apply a quadratic function of the form f(*x*) = *ax*2 + *bx* + *c* to each element *x* in the array.

The returned array must be in **sorted order**.

Expected time complexity: **O(n)**

**Example 1:**

```
Input: nums = [-4,-2,2,4], a = 1, b = 3, c = 5
Output: [3,9,15,33]
```

**Example 2:**

```
Input: nums = [-4,-2,2,4], a = -1, b = 3, c = 5
Output: [-23,-5,1,7] 
```





## Solution

```java
class Solution {
    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        int n = nums.length;
        int[] res = new int[n];
        for (int i = 0; i < n; i++) 
            nums[i] = a * nums[i] * nums[i] + b * nums[i] + c;
        
        int lo = 0, hi = nums.length - 1;
        
        
        if (a >= 0) {
            int i = n - 1;
            while(lo <= hi) 
                res[i--] = (nums[lo] >= nums[hi]) ? nums[lo++] : nums[hi--];
        } else {
            int i = 0;
            while(lo <= hi) 
                res[i++] = (nums[lo] <= nums[hi]) ? nums[lo++] : nums[hi--];
        }
        return res;
    }
}
```

