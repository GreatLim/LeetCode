# 323. Number of Connected Components in an Undirected Graph

## Description

Given `n` nodes labeled from `0` to `n - 1` and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.

**Example 1:**

```
Input: n = 5 and edges = [[0, 1], [1, 2], [3, 4]]

     0          3
     |          |
     1 --- 2    4 

Output: 2
```

**Example 2:**

```
Input: n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]]

     0           4
     |           |
     1 --- 2 --- 3

Output:  1
```

**Note:**
You can assume that no duplicate edges will appear in `edges`. Since all edges are undirected, `[0, 1]` is the same as `[1, 0]` and thus will not appear together in `edges`.

## Solution

```java
class Solution {
    public int countComponents(int n, int[][] edges) {
        HashMap<Integer, LinkedList<Integer>> G = new HashMap<>();
        boolean[] visited = new boolean[n];
        buildGraphy(G, edges);
        int res = 0;
        for(int i = 0; i < n; i++) {
            if(!visited[i]) res++;
            dfs(i, visited, G);
        }
        return res;
    }
    
    public void buildGraphy(HashMap<Integer, LinkedList<Integer>> G, int[][] edges) {
        for(int[] edge : edges) {
            int v = edge[0], w = edge[1];
            if(!G.containsKey(v)) G.put(v, new LinkedList<>());
            if(!G.containsKey(w)) G.put(w, new LinkedList<>());
            G.get(v).add(w);
            G.get(w).add(v);
        }
    }
    
    public void dfs(int v, boolean[] visited, HashMap<Integer, LinkedList<Integer>> G) {
        if(visited[v]) return;
        visited[v] = true;
        if(G.get(v) != null)
            for(int w : G.get(v)) {
                dfs(w, visited, G);
            }
    }
}
```

