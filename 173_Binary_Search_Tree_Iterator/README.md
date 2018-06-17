# 173. Binary Search Tree Iterator

## Description

Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling `next()` will return the next smallest number in the BST.

**Note:** `next()` and `hasNext()` should run in average O(1) time and uses O(*h*) memory, where *h* is the height of the tree.

**Credits:**
Special thanks to [@ts](https://oj.leetcode.com/discuss/user/ts) for adding this problem and creating all test cases.

## Solution

### Iterative version (Stack)

```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

public class BSTIterator {
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode cur;
    
    public BSTIterator(TreeNode root) {
        cur = root;
    }
    
    
    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !stack.isEmpty() || cur != null;
    }

    /** @return the next smallest number */
    public int next() {
        while(cur != null) {
            stack.push(cur);
            cur = cur.left;
        }
        cur = stack.pop();
        int res = cur.val;
        cur = cur.right;            
        return res;
    }
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = new BSTIterator(root);
 * while (i.hasNext()) v[f()] = i.next();
 */
```

### First try

```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

public class BSTIterator {
    LinkedList<Integer> list = new LinkedList<Integer>();
    Iterator<Integer> iterator;
    
    public BSTIterator(TreeNode root) {
        inorder(root);
        iterator = list.iterator();
    }
    
    public void inorder(TreeNode root) {
        if(root == null) return;
        inorder(root.left);
        list.add(root.val);
        inorder(root.right);
    }
    
    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return iterator.hasNext();
    }

    /** @return the next smallest number */
    public int next() {
        return iterator.next();
    }
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = new BSTIterator(root);
 * while (i.hasNext()) v[f()] = i.next();
 */
```