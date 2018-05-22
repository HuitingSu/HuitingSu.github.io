---
layout: post
title: Binary Search in 2D matrix
---

Just transfer it into 1D. Pay attention to the edge case. matrix == null || matrix.length == 0 || matrix[0].length == 0
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0) return false;
        int m = matrix.length;
        int n = matrix[0].length;
        int head = 0, tail = m * n - 1;
        while(head <= tail){
            int mid = head + (tail - head)/2;
            int row = mid / n;
            int col = mid % n;
            int mid_val = matrix[row][col];
            if(mid_val == target) return true;
            if(mid_val < target) head = mid + 1;
            else tail = mid - 1;
        }
        return false;
    }
}
```

