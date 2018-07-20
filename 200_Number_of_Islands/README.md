# 200. Number of Islands

##  Description

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input:
11110
11010
11000
00000

Output: 1
```

**Example 2:**

```
Input:
11000
11000
00100
00011

Output: 3
```



## Solution

### Concise Version

```java
class Solution {    
    public int numIslands(char[][] grid) {
        if(grid == null || grid.length == 0) return 0;
        int n = grid.length, m = grid[0].length, res = 0;
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if(grid[i][j] == '1') res++;
                dfs(grid, i, j);
            }
        }
        return res;
    }
    
    public void dfs(char[][] grid, int i, int j) {
        int n = grid.length, m = grid[0].length;
        if(i < 0 || i >= n || j < 0 || j >= m || grid[i][j] == '0') return;
        grid[i][j] = '0';
        dfs(grid, i + 1, j);
        dfs(grid, i - 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i, j - 1);
    }
}
```



### First Try (DFS)

```java
class Solution {
    public int num = 0;
    
    public int numIslands(char[][] grid) {
        if(grid == null || grid.length == 0) return 0;
        int n = grid.length;
        int m = grid[0].length;
        boolean[][] marked = new boolean[n][m];
        for(int i = 0; i < n; i++) 
            for(int j = 0; j < m; j++) 
                dfs(grid, marked, i, j, true);
        return num;
    }
    
    public void dfs(char[][] grid, boolean[][] marked, int i, int j, boolean firstTime) {
        int n = grid.length;
        int m = grid[0].length;
        if(i < 0 || i >= n || j < 0 || j >= m || marked[i][j] || grid[i][j] == '0') return;
        if(firstTime && !marked[i][j] && grid[i][j] == '1') num++;
        marked[i][j] = true;
        dfs(grid, marked, i + 1, j, false);
        dfs(grid, marked, i - 1, j, false);
        dfs(grid, marked, i, j + 1, false);
        dfs(grid, marked, i, j - 1, false);
    }
}
```

