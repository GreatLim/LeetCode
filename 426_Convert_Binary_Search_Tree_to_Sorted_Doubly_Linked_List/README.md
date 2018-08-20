# 426. Convert Binary Search Tree to Sorted Doubly Linked List

## Description

Convert a BST to a sorted circular doubly-linked list in-place. Think of the left and right pointers as synonymous to the previous and next pointers in a doubly-linked list.

Let's take the following BST as an example, it may help you understand the problem better:

![img](https://leetcode.com/static/images/problemset/BSTDLLOriginalBST.png)

We want to transform this BST into a circular doubly linked list. Each node in a doubly linked list has a predecessor and successor. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.

The figure below shows the circular doubly linked list for the BST above. The "head" symbol means the node it points to is the smallest element of the linked list.

![img](https://leetcode.com/static/images/problemset/BSTDLLReturnDLL.png)

Specifically, we want to do the transformation in place. After the transformation, the left pointer of the tree node should point to its predecessor, and the right pointer should point to its successor. We should return the pointer to the first element of the linked list.

The figure below shows the transformed BST. The solid line indicates the successor relationship, while the dashed line means the predecessor relationship.

![img](https://leetcode.com/static/images/problemset/BSTDLLReturnBST.png)



## Solution

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;

    public Node() {}

    public Node(int _val,Node _left,Node _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
    Node pre = null;
    public Node treeToDoublyList(Node root) {
        if(root == null) return null;
        Node sentinel = new Node(0, null, null);
        pre = sentinel;
        inorder(root);
        sentinel.right.left = pre;
        pre.right = sentinel.right;
        return sentinel.right;
    }
    
    public void inorder(Node root) {
        if(root == null) return;
        inorder(root.left);
        pre.right = root;
        root.left = pre;
        pre = root;
        inorder(root.right);
    }
    
}
```





## Note

* The value of `sentinel.right` is set only ONCE in `helper()` through `pre.right = cur;`, when `cur` point to the smallest node in the BST. After that, value of `pre` changes, so that `pre` and `dummy` do not point to the same node any more, which means value of `sentinel.right` stays pointing to the smallest node in the BST.