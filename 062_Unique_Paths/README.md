# 62. Unique Paths

## Description

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![img](https://leetcode.com/static/images/problemset/robot_maze.png)
Above is a 7 x 3 grid. How many possible unique paths are there?

**Note:** *m* and *n* will be at most 100.

**Example 1:**

```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```

**Example 2:**

```
Input: m = 7, n = 3
Output: 28
```

## Solution

```java
class Solution {
    public int uniquePaths(int m, int n) {        
        double res = 1;
        for(int i = 1; i <= n - 1; i++)
            res = res * (m - 1 + i) / i; 
        return (int) res;
    }
}
```



## Notes

* `res = res * (m - 1 + i) / i; ` is right, However, you can write it`res *=  (double) (m - 1 + i) / i;`

