# 238. Product of Array Except Self

## Description

Given an array `nums` of *n* integers where *n* > 1,  return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

**Example:**

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

**Note:** Please solve it **without division** and in O(*n*).

**Follow up:**
Could you solve it with constant space complexity? (The output array **does not** count as extra space for the purpose of space complexity analysis.)



## Solution

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int len = nums.length;
        int[] res = new int[len];
        for(int i = 0, temp = 1; i < len; i++) {
            res[i] = temp;
            temp *= num[i];
        }
        for(int i = len - 1, temp = 1; i >= 0; i--) {
            res[i] *= temp;
            temp *= num[i];
        }
        
        return res;
    }
}
```

