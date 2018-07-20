# 207. Course Schedule

##  Description

There are a total of *n* courses you have to take, labeled from `0` to `n-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, is it possible for you to finish all courses?

**Example 1:**

```
Input: 2, [[1,0]] 
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```

**Example 2:**

```
Input: 2, [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```

**Note:**

1. The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.

##  Crack

* 检测是否有环，可以建立 `onStack` 来追踪



## Solution

```java
class Solution {
    public boolean hasCycle = false;
    
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        LinkedList<Integer>[] G = new LinkedList[numCourses];
        boolean[] marked = new boolean[numCourses];
        boolean[] onStack = new boolean[numCourses];
        buildGraphy(G, prerequisites);
        for(int i = 0; i < numCourses; i++) {
            dfs(G, i, marked, onStack);
            if(hasCycle) return false;
        }
        return true;
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

