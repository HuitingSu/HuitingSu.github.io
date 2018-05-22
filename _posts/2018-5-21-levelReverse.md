Binary Tree Level Order Traversal II.

Use LinkedList to store the result!

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        if(root == null) return result;
        q.offer(root);
        
        while(!q.isEmpty()){
            List<Integer> level = new ArrayList<Integer>();   // be careful, need to new every time. Should not clear the list
            int n = q.size();
            
            for(int i = 1; i <= n; i++){
                TreeNode curr = q.poll();
                level.add(curr.val);
                if(curr.left != null) q.offer(curr.left);
                if(curr.right != null) q.offer(curr.right);
            }
            result.add(0, level);      
            //System.out.println(result);
        }
        return result;
    }
}
```

Notice that when you add list a to list b, you only pass the address. So if you clear list a, you will also clear list b.
One solution is to new a list in every iteration. Another solution is to new a list when you add.

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        List<Integer> level = new ArrayList<Integer>();
        if(root == null) return result;
        q.offer(root);
        
        while(!q.isEmpty()){
            int n = q.size();
            
            for(int i = 1; i <= n; i++){
                TreeNode curr = q.poll();
                level.add(curr.val);
                if(curr.left != null) q.offer(curr.left);
                if(curr.right != null) q.offer(curr.right);
            }
            result.add(0, new ArrayList<Integer>(level));
            level.clear();
            //System.out.println(result);
        }
        return result;
    }
}
```
