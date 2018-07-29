# 812. Largest Triangle Area

## Description

You have a list of points in the plane. Return the area of the largest triangle that can be formed by any 3 of the points.

```
Example:
Input: points = [[0,0],[0,1],[1,0],[0,2],[2,0]]
Output: 2
Explanation: 
The five points are show in the figure below. The red triangle is the largest.
```

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/04/1027.png)

**Notes:**

- `3 <= points.length <= 50`.
- No points will be duplicated.
-  `-50 <= points[i][j] <= 50`.
- Answers within `10^-6` of the true value will be accepted as correct.

## Solution

```java
class Solution {
    public double largestTriangleArea(int[][] points) {
        int[] up = points[0], bottom = points[0], right = points[0], left = points[0];
        double max = 0;
        for(int i = 0; i < points.length; i++) 
            for(int j = i + 1; j < points.length; j++) 
                for(int k = j + 1; k < points.length; k++) 
                    max = Math.max(area(points[i], points[j], points[k]), max);
        return max;
        
    }
    
    public double area(int[] A, int[] B, int[] C) {
        return 0.5 * Math.abs(A[0] * B[1] + B[0] * C[1] + C[0] * A[1]- B[0] * A[1] - C[0] * B[1] - A[0] * C[1]);
    }
}
```

