# 889. Construct Binary Tree from Preorder and Postorder Traversal

## Description

Return any binary tree that matches the given preorder and postorder traversals.

Values in the traversals `pre` and `post` are distinct positive integers.

 

**Example 1:**

```
Input: pre = [1,2,4,5,3,6,7], post = [4,5,2,6,7,3,1]
Output: [1,2,3,4,5,6,7]
```

 

**Note:**

- `1 <= pre.length == post.length <= 30`
- `pre[]` and `post[]` are both permutations of `1, 2, ..., pre.length`.
- It is guaranteed an answer exists. If there exists multiple answers, you can return any of them. 



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
    public TreeNode constructFromPrePost(int[] pre, int[] post) {
        int n = pre.length;
        return helper(pre, post, 0, n - 1, 0, n - 1);
    }
    
    public TreeNode helper(int[] pre, int[] post, int preStart, int preEnd, int postStart, int postEnd) {
        if(preStart > preEnd || preStart == -1 || preEnd == -1 || postStart == -1 || postEnd == -1) return null;
        TreeNode n = new TreeNode(pre[preStart]);
        
        int leftPreStart = -1, leftPreEnd = -1, leftPostStart = postStart, leftPostEnd = -1;
        int rightPreStart = -1, rightPreEnd = preEnd, rightPostStart = -1, rightPostEnd = -1;
        
        if()
        
        if(preStart + 1 < pre.length) {
            leftPreStart = preStart + 1;
            for(int i = postStart; i <= postEnd; i++) {
                if(post[i] == pre[leftPreStart]) leftPostEnd = i;
            }
            rightPostStart = leftPostEnd + 1;
        }
        
        if(postEnd - 1 >= 0) {
            rightPostEnd = postEnd - 1;
            for(int i = preStart; i <= preEnd; i++) {
                if(pre[i] == post[rightPostEnd]) rightPreStart = i;
            }
            leftPreEnd = rightPreStart - 1;
        }  

        
        n.left = helper(pre, post, leftPreStart, leftPreEnd, leftPostStart, leftPostEnd);
        n.right = helper(pre, post, rightPreStart, rightPreEnd, rightPostStart, rightPostEnd);
        
        return n;
    }
}
```

