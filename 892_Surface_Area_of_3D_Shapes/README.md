# 892. Surface Area of 3D Shapes

 On a `N * N` grid, we place some `1 * 1 * 1 `cubes.

Each value `v = grid[i][j]` represents a tower of `v` cubes placed on top of grid cell `(i, j)`.

Return the total surface area of the resulting shapes.

 


**Example 1:**

```
Input: [[2]]
Output: 10
```

**Example 2:**

```
Input: [[1,2],[3,4]]
Output: 34
```

**Example 3:**

```
Input: [[1,0],[0,2]]
Output: 16
```

**Example 4:**

```
Input: [[1,1,1],[1,0,1],[1,1,1]]
Output: 32
```

**Example 5:**

```
Input: [[2,2,2],[2,1,2],[2,2,2]]
Output: 46
```

 

**Note:**

- `1 <= N <= 50`
- `0 <= grid[i][j] <= 50`



## Solution

```java
class Solution {
    public int surfaceArea(int[][] grid) {
        int n = grid.length, m = grid[0].length;
        int res = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (grid[i][j] != 0) {
                    res += 2 + 4 * grid[i][j];
                    if(i >= 1) res -=  2 * Math.min(grid[i][j], grid[i - 1][j]);
                    if(j >= 1) res -=  2 * Math.min(grid[i][j], grid[i][j - 1]);
                }
            }
        }
        return res;
    }
}
```

