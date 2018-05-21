---
layout: post
title: Count Nodes in complete tree
---

Count the number of nodes in a complete binary tree.

Solution 1:
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
    public int countNodes(TreeNode root) {
        if(root == null) return 0;
        return checkNode(root, 0);
    }
    public int checkNode(TreeNode curr, int index){
        if(curr == null)
            return index;
        return Math.min(checkNode(curr.left, 2*index+1), checkNode(curr.right, 2*index+2));
    }
}
```
This solution is correct but the time complexity is O(n). We could find a more efficient solution using the properties of complete tree. 

```java
class Solution {
    public int countNodes(TreeNode root) {
        if(root == null) return 0;
        int hleft = getHeight(root.left);
        int hright = getHeight(root.right);
        if(hleft == hright)
            return (1 << hleft) -1 + 1 + countNodes(root.right);  
        else
            return (1 << hright) -1 + 1 + countNodes(root.left);
        
    }
    public int getHeight(TreeNode curr){
        if(curr == null) return 0; 
        return 1 + getHeight(curr.left);                
    }
}

```

Notice: In java, power is 1 << pow, ^ is Bitwise exclusive OR. The precedence of << is lower than +/-.

In this solution, I always check and compare the height of left subtree and right subtree. If they have the same height, it means the last node is in right subtree, then we don't need to traverse left subtree. If right subtree is shorter, that means the last node is in left subtree. In every step, I partition the tree into 2 subtree, so there are log(n) steps. In every step, getHeight is log(n). The time complexity is log(n)*log(n). 
