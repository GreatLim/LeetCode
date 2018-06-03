# 42. Trapping Rain Water

## Description

Given *n* non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![img](http://www.leetcode.com/static/images/problemset/rainwatertrap.png)
The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. **Thanks Marcos** for contributing this image!

**Example:**

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```



## Solution

### Dynamic Programing

```java
class Solution {
    public int trap(int[] height) {
        int size = height.length;
        int water = 0;
        if(size == 0) return water;
        int[] left = new int[size], right = new int[size];
        left[0] = height[0];
        right[size - 1] = height[size - 1];
        for (int i = 1; i < size; i++)
            left[i] = Math.max(height[i], left[i - 1]);
        for (int i = size - 2; i >= 0; i--) 
            right[i] = Math.max(height[i], right[i + 1]);
        for (int i = 1; i < size - 1; i++)
            water += Math.min(left[i], right[i]) - height[i];
        return water;
    }
}
```

### Brute Force

```java
class Solution {
    public int trap(int[] height) {
        int size = height.length;
        int water = 0;
        for (int i = 0; i < size; i++) {
            int left = 0, right = 0;
            for (int j = i; j < size; j++) 
                right = Math.max(right, height[j]);
            for (int j = i; j >= 0; j--) 
                left = Math.max(left, height[j]);
            water += Math.min(left, right) - height[i];
        }
        return water;
    }
}
```



## Notes

* to compute all the water,  you should know every index that can contain how much water
* you should determing the left_max & right_max including itself.