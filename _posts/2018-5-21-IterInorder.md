##  Binary Tree Inorder Traversal (Iterative)

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
    public List<Integer> inorderTraversal(TreeNode root) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> s = new Stack<TreeNode>();
        TreeNode curr = root;
        while(curr != null || !s.isEmpty()){
            if(curr!=null){
                s.push(curr);
                curr = curr.left;
            }
            else{
                curr = s.pop();
                result.add(curr.val);
                curr = curr.right;
            }    
        }
        return result;
    }
}
```

Pay attention to the arraylist methods and stack class. 
