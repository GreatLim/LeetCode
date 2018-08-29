# 894. All Possible Full Binary Trees

### 894. All Possible Full Binary Trees

[My Submissions](https://leetcode.com/contest/weekly-contest-99/problems/all-possible-full-binary-trees/submissions/)[Back to Contest](https://leetcode.com/contest/weekly-contest-99/)

- **User Accepted:**630
- **User Tried:**754
- **Total Accepted:**643
- **Total Submissions:**1141
- **Difficulty:**Medium

A *full binary tree* is a binary tree where each node has exactly 0 or 2 children.

Return a list of all possible full binary trees with `N` nodes.  Each element of the answer is the root node of one possible tree.

Each `node` of each tree in the answer **must** have `node.val = 0`.

You may return the final list of trees in any order.

 

**Example 1:**

```
Input: 7
Output: [[0,0,0,null,null,0,0,null,null,0,0],[0,0,0,null,null,0,0,0,0],[0,0,0,0,0,0,0],[0,0,0,0,0,null,null,null,null,0,0],[0,0,0,0,0,null,null,0,0]]
Explanation:
```

 ![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/08/22/fivetrees.png)

**Note:**

- `1 <= N <= 20`

## Solution

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
    public List<TreeNode> allPossibleFBT(int N) {
        List<TreeNode> res = new LinkedList<>();
        if(N == 1) {
            res.add(new TreeNode(0));
            return res;
        }
        for(int i = 1; i <= N - 1; i+=2) {
            List<TreeNode> rightList = allPossibleFBT(i);
            List<TreeNode> leftList = allPossibleFBT(N - 1 - i);
            for(TreeNode right : rightList) {
                for(TreeNode left : leftList) {
                    TreeNode root = new TreeNode(0);
                    root.left = clone(left);
                    root.right = clone(right);
                    res.add(root);
                }
            }
        }
        return res;
    }
    
    public TreeNode clone(TreeNode root) {
        if(root == null) return null;
        TreeNode cloneRoot = new TreeNode(0);
        cloneRoot.left = clone(root.left);
        cloneRoot.right = clone(root.right);
        return cloneRoot;
    }
    
}
```



