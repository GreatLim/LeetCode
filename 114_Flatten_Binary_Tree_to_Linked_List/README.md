# 114. Flatten Binary Tree to Linked List

## Description

Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:

```
    1
   / \
  2   5
 / \   \
3   4   6
```

The flattened tree should look like:

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```



## Solution

### Concise Version 

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
    private TreeNode prev;
    
    public void flatten(TreeNode root) {
        if(root == null) return;
        flatten(root.right);
        flatten(root.left);
        root.right = prev;
        root.left = null;
        prev = root;
    }
}
```



### First Try (inorder)

``` java
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
    public void flatten(TreeNode root) {
        if(root == null) return;
        flatten(root.left);
        if(root.left != null && root.left.left == null) {
            TreeNode temp = root.right;
            root.right = root.left;
            root.left = null;
            while(root.right != null) 
                root = root.right;
            root.right = temp;
        }
        flatten(root.right);
    }
}
```



## Notes

* use instance variable to record PREV to make code more concise
* the process of concise verison

```
    1
   / \
  2   5
 / \   \
3   4   6
-----------        
pre = 5
cur = 4

    1
   / 
  2   
 / \   
3   4
     \
      5
       \
        6
-----------        
pre = 4
cur = 3

    1
   / 
  2   
 /   
3 
 \
  4
   \
    5
     \
      6
-----------        
cur = 2
pre = 3

    1
   / 
  2   
   \
    3 
     \
      4
       \
        5
         \
          6
-----------        
cur = 1
pre = 2

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

