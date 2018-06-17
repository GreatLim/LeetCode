# 84. Largest Rectangle in Histogram

## Description

Given *n* non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![img](https://leetcode.com/static/images/problemset/histogram.png)
Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.

 

![img](https://leetcode.com/static/images/problemset/histogram_area.png)
The largest rectangle is shown in the shaded area, which has area = `10` unit.

## Solution

### Stack

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int max = 0;
        int h = 0, w = 0;
        // the stack records indexes!!!
        Stack<Integer> stack = new Stack<Integer>();
        for(int i = 0; i < heights.length; i++) {
            while(!stack.isEmpty() && heights[stack.peek()] > heights[i]) {
                h = heights[stack.pop()];
                w = stack.isEmpty() ? i : (i - stack.peek() - 1);
                max = Math.max(h * w, max);
            }
            stack.push(i);
        }
        
        while(!stack.isEmpty()) {
            h = heights[stack.pop()];
            w = stack.isEmpty() ? heights.length : (heights.length - stack.peek() - 1);
            // System.out.println(h + " " + w);
            max = Math.max(h * w, max);
        }
        return max;
    }
}
```



### Brute force

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int max = 0;
        for (int i = 0; i < heights.length; i++) {
            int start = i;
            int end = i;
            while(start >= 0 && heights[start] >= heights[i]) start--;
            while(end < heights.length && heights[end] >= heights[i]) end++;
            max = Math.max(max, (end - start - 1) * heights[i]);
        }
        return max;
    }
}
```





## Notes

* We need to know index of the first smaller (smaller than ‘x’) bar on left of ‘x’ and index of first smaller bar on right of ‘x’. Let us call these indexes as ‘left index’ and ‘right index’ respectively.
* for explanation, please see <http://www.geeksforgeeks.org/largest-rectangle-under-histogram/>
* the stack stores indexes



## Link

**stack** 496_Next_Greater_Element_I