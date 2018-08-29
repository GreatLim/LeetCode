# 515. Find Largest Value in Each Tree Row

## Description

You need to find the largest value in each row of a binary tree.

**Example:**

```
Input: 

          1
         / \
        3   2
       / \   \  
      5   3   9 

Output: [1, 3, 9]
```

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
    public List<Integer> largestValues(TreeNode root) {
        Queue<TreeNode> q = new LinkedList<>();
        List<Integer> res = new LinkedList<>();
        if(root == null) return res;
        q.offer(root);
        while (!q.isEmpty()) {
            int size = q.size(), temp = Integer.MIN_VALUE;
            for (int i = 0; i < size; i++) {
                TreeNode n = q.poll();
                if(n.val > temp) temp = n.val;
                if(n.left != null) q.offer(n.left);
                if(n.right != null) q.offer(n.right);
            }
            res.add(temp);
        }
        return res;
    }
}
```

