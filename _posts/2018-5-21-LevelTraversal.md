---
layout: post
title: Average of Levels in Binary Tree
---

Use BFS.
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
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> result = new ArrayList<Double>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();  //Need to use LinkedList to implement queue
        
        if(root == null) return result;
        q.offer(root);
        while(!q.isEmpty()){
            double sum = 0;
            int length = q.size();
            for(int i = 1; i <= length; i++){          //notice here, for different level
                TreeNode curr = q.poll();                   //poll is remove head, can declare when use
                if(curr.left != null) q.offer(curr.left);   //offer is append
                if(curr.right != null) q.offer(curr.right);
                sum += curr.val;
            }
            result.add(sum / length);    //add is append for array
        }
        return result;
    }
}
```
