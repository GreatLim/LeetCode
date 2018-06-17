# 59. Spiral Matrix II

## Description

Given a positive integer *n*, generate a square matrix filled with elements from 1 to *n*2 in spiral order.

**Example:**

```
Input: 3
Output:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

## Solution

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int num = 1;
        int[][] res = new int[n][n];
        int left = 0, right = n - 1;
        int up = 0, down = n - 1;
        while(left <= right || up <= down) {
            for(int i = left; i <= right; i++)
                res[up][i] = num++;
            for(int i = up + 1; i <= down; i++)
                res[i][right] = num++;
            for(int i = right - 1; i >= left; i--)
                res[down][i] = num++;
            for(int i = down - 1; i >= up + 1; i--)
                res[i][left] = num++;
            left++;
            right--;
            up++;
            down--;
        }
        return res;
    }
}
```

