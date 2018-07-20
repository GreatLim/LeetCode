# 210. Course Schedule II

## Description

There are a total of *n* courses you have to take, labeled from `0` to `n-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

**Example 1:**

```
Input: 2, [[1,0]] 
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished   
             course 0. So the correct course order is [0,1] .
```

**Example 2:**

```
Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both     
             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. 
             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```

**Note:**

1. The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.

##  Solution

### DFS


```java
class Solution {
    public boolean hasCycle = false;
    public int[] order;
    public int i = 0;
    
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        LinkedList<Integer>[] G = new LinkedList[numCourses];
        order = new int[numCourses];
        boolean[] marked = new boolean[numCourses];
        boolean[] onStack = new boolean[numCourses];
        buildGraphy(G, prerequisites);
        for(int i = 0; i < numCourses; i++) {
            dfs(G, i, marked, onStack);
            if(hasCycle) return new int[0];
        }
        return order;
    }

    public void dfs(LinkedList<Integer>[] G, int v, boolean[] marked, boolean[] onStack) {
        if(onStack[v]) {
            hasCycle = true;
            return;
        }
        if(marked[v]) return;
        onStack[v] = true;
        marked[v] = true;
        if(G[v] != null)
            for(int w : G[v]) 
                dfs(G, w, marked, onStack);
        order[i++] = v;
        onStack[v] = false;
    }
    
    
    public void buildGraphy(LinkedList<Integer>[] G, int[][] prerequisites) {
        for(int i = 0; i < prerequisites.length; i++) {
            int v = prerequisites[i][0];
            int w = prerequisites[i][1];
            if(G[v] == null) G[v] = new LinkedList<Integer>();
            G[v].add(w);
        }
    }
}
```

