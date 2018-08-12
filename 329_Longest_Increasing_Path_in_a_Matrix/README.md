# 329. Longest Increasing Path in a Matrix

## Description

Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary (i.e. wrap-around is not allowed).

**Example 1:**

```
Input: nums = 
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
] 
Output: 4 
Explanation: The longest increasing path is [1, 2, 6, 9].
```

**Example 2:**

```
Input: nums = 
[
  [3,4,5],
  [3,2,6],
  [2,2,1]
] 
Output: 4 
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed. 
```



## Solution

```java
class Solution {
    public int longestIncreasingPath(int[][] matrix) {
        if(matrix.length == 0 || matrix == null) return 0;
        int n = matrix.length, m = matrix[0].length;
        int[][] cache = new int[n][m];
        int res = 0;
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                int len = dfs(i, j, -1, -1, matrix, cache);
                res = Math.max(len, res);
            }
        }
        return res;
    }
    
    public int dfs(int i, int j, int pi, int pj, int[][] matrix, int[][] cache) {
        int n = matrix.length, m = matrix[0].length;
        if(i >= n || i < 0 || j >= m || j < 0) return 0;
        if(pi >= 0 && pj >= 0 && matrix[i][j] <= matrix[pi][pj]) return 0;
        if(cache[i][j] != 0) return cache[i][j];
        int max = 1;
        int up = dfs(i + 1, j, i, j, matrix, cache);
        int bottom = dfs(i - 1, j, i, j, matrix, cache);
        int right = dfs(i, j + 1, i, j, matrix, cache);
        int left = dfs(i, j - 1, i, j, matrix, cache);
        max = max + Math.max(Math.max(up, bottom), Math.max(left, right));
        cache[i][j] = max;
        return max;
    }
}
```



## Note

To get max length of increasing sequences:

1. Do `DFS` from every cell
2. Compare every 4 direction and skip cells that are out of boundary or smaller
3. Get matrix `max` from every cell's `max`
4. Use `matrix[x][y] <= matrix[i][j]` so we don't need a `visited[m][n]` array
5. The key is to `cache` the distance because it's highly possible to revisit a cell

Hope it helps!

