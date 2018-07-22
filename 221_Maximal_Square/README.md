# 221.  Maximal Square

## Description

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

**Example:**

```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```

## Solution

### DP

```java
class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix == null || matrix.length == 0) return 0;
        int n = matrix.length, m = matrix[0].length;
        int max = 0;
        int[] pre = new int[m];
        for(int i = 0; i < n; i++) {
            int[] cur = new int[m];
            for(int j = 0; j < m; j++) {
                if(matrix[i][j] == '1') {
                    int left = (j >= 1) ? cur[j - 1] : 0;
                    int up = (i >= 1) ? pre[j] : 0;
                    int dig = (i >= 1 && j >= 1) ? pre[j - 1] : 0;
                    cur[j] = Math.min(Math.min(left, up), dig) + 1;
                    max = Math.max(max, cur[j] * cur[j]);
                }
            }
            pre = cur;
        }
        return max;
    }
}
```



### Maximal Rectangle Version

```java
class Solution {
    public int maximalSquare(char[][] matrix) {
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
            for(int j = 0; j < m; j++) {
                int l = Math.min((right[j] - left[j]) , height[j]);
                max = Math.max(max, l * l);
            }
        }
        return max;
    }
}
```

