---
layout: post
title: kth Smallest Number
---

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        PriorityQueue<Integer> q =  new PriorityQueue<Integer>(k, new Comparator<Integer>(){
            public int compare(Integer a, Integer b) {
                return matrix[a/n][a%n] - matrix[b/n][b%n];   // need to compare the value in matrix, not index!
            }
        });
        boolean[] visited = new boolean[n*n];   // not n*n-1
        q.offer(0);
        int count = 0;
        while(count < k){
            int index = q.poll();
            count ++;
            if(count == k) return matrix[index/n][index%n];

            if(index % n < n-1 && !visited[index + 1]){
                q.offer(index + 1);
                visited[index + 1] = true;
            }
            if(index / n < n-1 && !visited[index + n]){
                q.offer(index + n);
                visited[index + n] = true;
            }
        }
        return 0;
    }
}
```

Can also use tuple here.
```java
public Tuple (int x, int y, int val) {
        this.x = x;
        this.y = y;
        this.val = val;
    }
```
