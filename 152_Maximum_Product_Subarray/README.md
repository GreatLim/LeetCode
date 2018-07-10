# 152. Maximum Product Subarray

##  Description

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

**Example 1:**

```
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**

```
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```

## Solution

```java
class Solution {
    public int maxProduct(int[] nums) {
        int maxSoFar = nums[0];
        int minHerePre = 1, maxHerePre = 1;
        int maxHere, minHere;
        for(int num : nums) {
            maxHere = Math.max(Math.max(maxHerePre * num, minHerePre * num), num);
            minHere = Math.min(Math.min(maxHerePre * num, minHerePre * num), num);
            maxSoFar = Math.max(maxHere, maxSoFar);
            maxHerePre = maxHere;
            minHerePre = minHere;
        }
        return maxSoFar;
    }
}
```

