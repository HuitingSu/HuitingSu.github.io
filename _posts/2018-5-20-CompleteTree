Decide whether the binary tree is complete or not.

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null)return true;
        int head = 0, tail = 0;
        boolean isNull = false;
        TreeNode[] q;
        q = new TreeNode[1000];    //Declaring array
        q[0] = root;
        while(head <= tail){
            if(q[head] != null){
                tail += 1;
                q[tail] = q[head].left;
                if(isNull == true && q[tail] != null)
                    return false;
                if(isNull == false && q[tail] == null)
                    isNull = true;
                tail += 1;
                q[tail] = q[head].right;
                if(isNull == true && q[tail] != null)
                    return false;
                if(isNull == false && q[tail] == null)
                    isNull = true;
            }
            head += 1;
        }
        return true;
    }
}
```
