# 366. Find Leaves of Binary Tree

## Description

Given a binary tree, collect a tree's nodes as if you were doing this: Collect and remove all leaves, repeat until the tree is empty.

 

**Example:**

```
Input: [1,2,3,4,5]
  
          1
         / \
        2   3
       / \     
      4   5    

Output: [[4,5,3],[2],[1]]
```

 

**Explanation:**

\1. Removing the leaves `[4,5,3]` would result in this tree:

```
          1
         / 
        2          
```

 

\2. Now removing the leaf `[2]` would result in this tree:

```
          1          
```

 

\3. Now removing the leaf `[1]` would result in the empty tree:

```
          []         
```



## Solution

### Other Solution

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        height(root, res);
        return res;
    }
    
    public int height(TreeNode root, List<List<Integer>> res) {
        if (root == null) return -1;
        int height = Math.max(height(root.left, res), height(root.right, res)) + 1;
        if(height > res.size() - 1) res.add(new LinkedList<>());
        res.get(height).add(root.val);
        return height;
    }
}
```



### First Try

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> findLeaves(TreeNode root) {
        if(root == null) return new LinkedList<>();;
        List<List<Integer>> left = findLeaves(root.left);
        List<List<Integer>> right = findLeaves(root.right);
        List<List<Integer>> res = combine(left, right);
        res.add(new LinkedList<>());
        res.get(res.size() - 1).add(root.val);
        return res;
    }
    
    public List<List<Integer>> combine(List<List<Integer>> left, List<List<Integer>> right) {
        for (int i = 0; i < Math.max(left.size(), right.size()); i++) {
            if(i >= left.size()) left.add(new LinkedList<>());
            if(i < right.size()) left.get(i).addAll(right.get(i));
        }
        return left;
    }
}
```

