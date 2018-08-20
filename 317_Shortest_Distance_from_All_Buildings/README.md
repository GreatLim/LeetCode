# 317. Shortest Distance from All Buildings

## Description

You want to build a house on an *empty* land which reaches all buildings in the shortest amount of distance. You can only move up, down, left and right. You are given a 2D grid of values **0**, **1** or **2**, where:

- Each **0** marks an empty land which you can pass by freely.
- Each **1** marks a building which you cannot pass through.
- Each **2** marks an obstacle which you cannot pass through.

**Example:**

```
Input: [[1,0,2,0,1],[0,0,0,0,0],[0,0,1,0,0]]

1 - 0 - 2 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0

Output: 7 

Explanation: Given three buildings at (0,0), (0,4), (2,2), and an obstacle at (0,2),
             the point (1,2) is an ideal empty land to build a house, as the total 
             travel distance of 3+3+1=7 is minimal. So return 7.
```

**Note:**
There will be at least one building. If it is not possible to build such house according to the above rules, return -1.

 

## Solution

```java
class Solution {
    public int shortestDistance(int[][] grid) {
        if(grid == null || grid.length == 0) return -1;
        int n = grid.length, m = grid[0].length;
        int numOfBuilding = 0;
        int[][] distances = new int[n][m];
        int[][] reach = new int[n][m];
        int res = Integer.MAX_VALUE;
        
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if(grid[i][j] == 1) numOfBuilding++;
                if(grid[i][j] == 0) {
                    boolean[][] isVisited = new boolean[n][m];
                    int depth = 0;
                    Queue<int[]> q = new LinkedList<>();
                    q.offer(new int[]{i, j});
                    while(!q.isEmpty()) {
                        int size = q.size();
                        for(int k = 0; k < size; k++) {
                            int[] v = q.poll();
                            int x = v[0], y = v[1];
                            if(x < 0 || y < 0 || x >= n || y >= m || isVisited[x][y]) continue;
                            isVisited[x][y] = true;
                            if(grid[x][y] == 1) {
                                reach[i][j] ++;
                                distances[i][j] += depth;

                            } else if(grid[x][y] == 0) {
                                q.offer(new int[]{x - 1, y});
                                q.offer(new int[]{x + 1, y});
                                q.offer(new int[]{x, y - 1});
                                q.offer(new int[]{x, y + 1});
                            }
                        }
                        depth++;
                    }
                    
                }
            }
        }
        
        
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {                
                if(reach[i][j] == numOfBuilding) 
                    res = Math.min(res, distances[i][j]);
            }
        }
        
        if(res == Integer.MAX_VALUE) return -1;
        return res;
    }
}
```

