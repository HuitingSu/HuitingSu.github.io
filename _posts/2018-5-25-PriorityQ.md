---
layout: post
title: kth Smallest Number
---
For min_heap, the comparator should be implemented in such a way that it returns negative int if first argument is less than the second one and returns zero if they are equal and positive int if first argument is greater than second one.

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
