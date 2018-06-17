# 63. Unique Paths II

## Description

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

![img](https://leetcode.com/static/images/problemset/robot_maze.png)

An obstacle and empty space is marked as `1` and `0` respectively in the grid.

**Note:** *m* and *n* will be at most 100.

**Example 1:**

```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```



## Solution

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int width = obstacleGrid[0].length;
        int height = obstacleGrid.length;
        int[][] dp = new int[height][width];
        for(int i = 0; i < height; i ++) {
            if(obstacleGrid[i][0] == 1) break;
            dp[i][0] = 1;
        }
        for(int j = 0; j < width; j ++) {
            if(obstacleGrid[0][j] == 1) break;
            dp[0][j] = 1;
        }
        for(int i = 1; i < height; i++) {
            for(int j = 1; j < width; j++) {
                if(obstacleGrid[i][j] == 1) dp[i][j] = 0;
                else dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[height - 1][width - 1];
    }
}
```

