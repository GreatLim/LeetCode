# 117. Populating Next Right Pointers in Each Node II

## Description

Given a binary tree

```
struct TreeLinkNode {
  TreeLinkNode *left;
  TreeLinkNode *right;
  TreeLinkNode *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

**Note:**

- You may only use constant extra space.
- Recursive approach is fine, implicit stack space does not count as extra space for this problem.

**Example:**

Given the following binary tree,

```
     1
   /  \
  2    3
 / \    \
4   5    7
```

After calling your function, the tree should look like:

```
     1 -> NULL
   /  \
  2 -> 3 -> NULL
 / \    \
4-> 5 -> 7 -> NULL
```

## Crack

给每一行设置`sentinel`和`node`，用链表的方法进行连接

## Solution

### Concise Version

```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        while(root != null) {
            TreeLinkNode sentinel = new TreeLinkNode(0);
            TreeLinkNode node = sentinel;
            while(root != null) {
                if(root.left != null) {
                    node.next = root.left;
                    node = node.next;
                }
                if(root.right != null) {
                    node.next = root.right;
                    node = node.next;
                }
                root = root.next;
            }
            root = sentinel.next;
        }
    }
}
```

### First Try

```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        if(root == null) return;
        boolean hasNextFirstNode = false;
        TreeLinkNode nextFirstNode = null;
        while(root != null) {
            if(root.left != null) {
                if(!hasNextFirstNode) {
                    hasNextFirstNode = true;
                    nextFirstNode = root.left;
                }
                if(root.right != null) root.left.next = root.right;
                else root.left.next = findNextNode(root.next);
            }
            if(root.right != null) {
                if(!hasNextFirstNode) {
                    hasNextFirstNode = true;
                    nextFirstNode = root.right;
                }
                root.right.next = findNextNode(root.next);
            }
            root = root.next;
        }
        connect(nextFirstNode);
    }
    
    private TreeLinkNode findNextNode(TreeLinkNode root) {
        if(root == null) return null;
        TreeLinkNode node = null;
        while(root != null) {
            if(root.left != null) {
                node = root.left;
                break;
            }
            if(root.right != null) {
                node = root.right;
                break;
            }
            root = root.next;
        }
        return node;
    }
}
```

