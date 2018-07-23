# 169. Majority Element

## Description

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```
Input: [3,2,3]
Output: 3
```

**Example 2:**

```
Input: [2,2,1,1,1,2,2]
Output: 2
```

## Solution

```java
class Solution {
    public int majorityElement(int[] nums) {
        int candidate = nums[0], count = 0;
        int limit = nums.length / 2;
        for(int num : nums) {
            if(candidate == num) count++;
            else if(count == 0) {
                candidate = num;
                count = 1;
            } else count--;
        }
        return candidate;

    }
}
```

