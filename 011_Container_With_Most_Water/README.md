# 11. Container With Most Water

## Description
Given *n* non-negative integers *a1*, *a2*, ..., *an*, where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and *n* is at least 2.

##Solution
```java
class Solution {
    public int maxArea(int[] height) {
        int maxArea = 0;
        int left = 0;
        int right = height.length - 1;
        while(right > left) {
            int width = right - left;
            if(height[left] > height[right]) {
                maxArea = Math.max(height[right] * width, maxArea);
                right --;
            } else {
                maxArea = Math.max(height[left] * width, maxArea);
                left ++;                
            }
        }
        return maxArea;
    }
}
```


