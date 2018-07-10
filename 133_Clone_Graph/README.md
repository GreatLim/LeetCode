# 133. Clone Graph

 Clone an undirected graph. Each node in the graph contains a `label` and a list of its `neighbors`.

 

OJ's undirected graph serialization:

Nodes are labeled uniquely. `#` `,` As an example, consider the serialized graph `{0,1,2#1,2#2,2}`.

The graph has a total of three nodes, and therefore contains three parts as separated by `#`.

1. First node is labeled as `0`. Connect node `0` to both nodes `1` and `2`.
2. Second node is labeled as `1`. Connect node `1` to node `2`.
3. Third node is labeled as `2`. Connect node `2` to node `2` (itself), thus forming a self-cycle.

Visually, the graph looks like the following:

```
       1
      / \
     /   \
    0 --- 2
         / \
         \_/
```
## Crack

哈希之，然后dfs

建立hash表的时候 key 为 label (unique), value为对应的cloneNode

## Solution

### dfs

```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     List<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if(node == null) return null;
        HashMap<Integer, UndirectedGraphNode> marked = new HashMap<Integer, UndirectedGraphNode>();
        UndirectedGraphNode cloneNode = new UndirectedGraphNode(node.label);
        dfs(node, cloneNode, marked);
        return cloneNode;
    }
    
    public void dfs(UndirectedGraphNode node, UndirectedGraphNode cloneNode, HashMap<Integer, UndirectedGraphNode> marked) {
        if(marked.containsKey(node.label)) return;
        marked.put(node.label, cloneNode);
        for(UndirectedGraphNode adj : node.neighbors) {
            UndirectedGraphNode cloneAdj = marked.getOrDefault(adj.label, new UndirectedGraphNode(adj.label));
            cloneNode.neighbors.add(cloneAdj);
            dfs(adj, cloneAdj, marked);
        }
    }
}
```

