# 85. Maximal Rectangle

## Desription

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

**Example:**

```
Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6
```

## Crack

* `"1"` 的 `left` 和 `right` 是受到上一行的约束
  - 如果上一行是 `"0"` 则没有约束
  - 如果上一行是 `"1"` 则 `left` 要大于上一行的 `left`，`right` 要小于上一行的 `right`
* `"0"` 的 `left` 是 0 和 `right` 是 m

## Solution

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if(matrix.length == 0) return 0;
        int n = matrix.length;
        int m = matrix[0].length;
        int max = 0;
        int[] height = new int[m], left = new int[m], right = new int[m];
        for(int j = 0; j < m; j++) right[j] = m;
        for (int i = 0; i < n; i++) {
            int curLeft = 0, curRight = m;
            for(int j = 0; j < m; j++) {
                if(matrix[i][j] == '1') height[j] = height[j] + 1;
                else height[j] = 0;
            } 
            for(int j = 0; j < m; j++) {
                if(matrix[i][j] == '1') left[j] = Math.max(curLeft, left[j]);
                else {
                    curLeft = j + 1;
                    left[j] = 0;
                }
            }
            for(int j = m - 1; j >= 0; j--) {
                if(matrix[i][j] == '1') right[j] = Math.min(curRight, right[j]);
                else {
                    curRight = j;
                    right[j] = m;
                }
                
            }
            for(int j = 0; j < m; j++) 
                max = Math.max(max, (right[j] - left[j]) * height[j]);
        }
        return max;
    }
}
```