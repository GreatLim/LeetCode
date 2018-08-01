# 105. Construct Binary Tree from Preorder and Inorder Traversal

## Description

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**
You may assume that duplicates do not exist in the tree.

For example, given

```
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
```

Return the following binary tree:

```
    3
   / \
  9  20
    /  \
   15   7
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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return buildTree(preorder, 0, inorder, 0, inorder.length - 1);
    }
    
    public TreeNode buildTree(int[] preorder, int preStart, int[] inorder, int inStart, int inEnd) {
        if(preStart > preorder.length || inStart > inEnd) return null;
        int index = 0;
        for(int i = inStart; i <= inEnd; i++) {
            if(inorder[i] ==  preorder[preStart]) {
                index = i;
                break;
            }
        }
        TreeNode n = new TreeNode(inorder[index]);
        
        n.left = buildTree(preorder, preStart + 1, inorder, inStart, index - 1);
        n.right = buildTree(preorder, preStart + index - inStart + 1, inorder, index + 1, inEnd);
        
        return n;
    }
}
```



## Notes

Let us look at this example tree.

```
        _______7______
       /              \
    __10__          ___2
   /      \        /
   4       3      _8
            \    /
             1  11
```

The preorder and inorder traversals for the binary tree above is:

```
preorder = {7,10,4,3,1,2,8,11}
inorder = {4,10,3,1,7,11,8,2}
```

The crucial observation to this problem is *the tree’s root always coincides with the first element in preorder traversal*. This must be true because in preorder traversal you always traverse the root node before its children. The root node’s value appear to be **7** from the binary tree above.

We easily find that **7** appears as the 4th index in the inorder sequence. (Notice that earlier we assumed that duplicates are not allowed in the tree, so there would be no ambiguity). For inorder traversal, we visit the left subtree first, then root node, and followed by the right subtree. Therefore, all elements left of **7** must be in the left subtree and all elements to the right must be in the right subtree.

We see a clear recursive pattern from the above observation. After creating the root node (**7**), we construct its left and right subtree from inorder traversal of {4, 10, 3, 1} and {11, 8, 2} respectively. We also need its corresponding preorder traversal which could be found in a similar fashion. If you remember, preorder traversal follows the sequence of root node, left subtree and followed by right subtree. Therefore, the left and right subtree’s postorder traversal must be {10, 4, 3, 1} and {2, 8, 11} respectively. Since the left and right subtree are binary trees in their own right, we can solve recursively!

We left out some details on how we search the root value’s index in the inorder sequence. How about a simple *linear search*? If we assume that the constructed binary tree is always balanced, then we can guarantee the run time complexity to be O(*N*log *N*), where *N* is the number of nodes. However, this is not necessarily the case and the constructed binary tree can be skewed to the left/right, which has the worst complexity of O(*N*2).

A more efficient way is to eliminate the search by using an efficient look-up mechanism such as *hash table*. By hashing an element’s value to its corresponding index in the inorder sequence, we can do look-ups in constant time. Now, we need only O(*N*) time to construct the tree, which theoretically is the most efficient way.