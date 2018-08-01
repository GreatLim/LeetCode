# 695. Max Area of Island

## Description

Given a non-empty 2D array `grid` of 0's and 1's, an **island** is a group of `1`'s (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

**Example 1:**

```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```

Given the above grid, return 

```
6
```

. Note the answer is not 11, because the island must be connected 4-directionally.

**Example 2:**

```
[[0,0,0,0,0,0,0,0]]
```

Given the above grid, return 

```
0
```

.

**Note:** The length of each dimension in the given `grid` does not exceed 50.



## Solution

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        if(grid == null || grid.length == 0) return 0;
        int n = grid.length, m = grid[0].length, res = 0;
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                res = Math.max(dfs(grid, i, j), res);
            }
        }
        return res;
    }
    

    
    public int dfs(int[][] grid, int i, int j) {
        int n = grid.length, m = grid[0].length;
        if(i < 0 || i >= n || j < 0 || j >= m || grid[i][j] == 0) return 0;
        grid[i][j] = 0;
        int up = dfs(grid, i + 1, j);
        int bottom = dfs(grid, i - 1, j);
        int right = dfs(grid, i, j + 1);
        int left = dfs(grid, i, j - 1);
        return up + bottom + right + left + 1;
    }
    
}
```

