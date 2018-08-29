# 286. Walls and Gates

## Description

You are given a *m x n* 2D grid initialized with these three possible values.

1. `-1` - A wall or an obstacle.
2. `0` - A gate.
3. `INF` - Infinity means an empty room. We use the value `231 - 1 = 2147483647` to represent `INF` as you may assume that the distance to a gate is less than `2147483647`.

Fill each empty room with the distance to its *nearest* gate. If it is impossible to reach a gate, it should be filled with `INF`.

**Example:** 

Given the 2D grid:

```
INF  -1  0  INF
INF INF INF  -1
INF  -1 INF  -1
  0  -1 INF INF
```

After running your function, the 2D grid should be:

```
  3  -1   0   1
  2   2   1  -1
  1  -1   2  -1
  0  -1   3   4
```



## Crack

* multiple source BFS
* use `rooms[x - 1][y] == Integer.MAX_VALUE` to judge whether this vertex has been reached.



## Solution

```java
class Solution {
    public void wallsAndGates(int[][] rooms) {
        if(rooms.length == 0 || rooms == null) return;
        int n = rooms.length, m = rooms[0].length;
        Queue<int[]> q = new LinkedList<>();
        
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (rooms[i][j] == 0) q.offer(new int[]{i, j});
            }
        }
        
        while (!q.isEmpty()) {
            int[] v = q.poll();
            int x = v[0], y = v[1];
            if(x > 0 && rooms[x - 1][y] == Integer.MAX_VALUE) {
                rooms[x - 1][y] = rooms[x][y] + 1;
                q.offer(new int[]{x - 1, y});
            }
            if(x < n - 1 && rooms[x + 1][y] == Integer.MAX_VALUE) {
                rooms[x + 1][y] = rooms[x][y] + 1;
                q.offer(new int[]{x + 1, y});
            }
            if(y > 0 && rooms[x][y - 1] == Integer.MAX_VALUE) {
                rooms[x][y - 1] = rooms[x][y] + 1;
                q.offer(new int[]{x, y - 1});
            }
            if(y < m - 1 && rooms[x][y + 1] == Integer.MAX_VALUE) {
                rooms[x][y + 1] = rooms[x][y] + 1;
                q.offer(new int[]{x, y + 1});
            }
        }
        
    }
}
```

