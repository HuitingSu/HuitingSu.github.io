---
layout: post
title: Search in Rotated Arrays
---

## Problem 1
Find the minimum value in the array. Think about the cases. 

Actually it can be more concise:
```java
class Solution {
    public int findMin(int[] nums) {
        if(nums == null || nums.length == 0) return -1;
        int min = nums[0];
        int head = 0, tail = nums.length - 1;
        while(head <= tail){
            int mid = head + (tail - head) / 2;
            min = Math.min(min, nums[mid]);
            if(nums[mid] > nums[tail]) head = mid + 1;
            else tail = mid - 1;
        }
        return min;
    }
}
```

## Problem 2
Following up problem 1: Consider duplicated numbers.

Solution 1:
```java
class Solution {
    public int findMin(int[] nums) {
        if(nums == null || nums.length == 0) return -1;
        int min = nums[0];
        int head = 0, tail = nums.length - 1;
        while(head <= tail){
            int mid = head + (tail - head) / 2;
            min = Math.min(min, nums[mid]);
            if(nums[mid] == nums[head] && nums[mid] == nums[tail]) return min;
            if(nums[mid] >= nums[head] && nums[mid] >= nums[tail]) head = mid + 1;
            else tail = mid - 1;
        }
        return min;
    }
}
```
The problem of this solution is, when it is [7, 8, 10, 10, 10], it will search the right part of the array, which is incorrect.

Change the way of thinking: only when the mid is larger than tail, we need to search the right part, and mid is surely not the minimum. 
In this case we can set head = mid + 1.  
In other cases, we want to search left, but the mid value can still be the minimum, so keep that value. tail = mid.

Think: all sub-arrays are still rotated, if mid is less than right, than search left; if mid is larger than right, search right. 
When mid is equal to right, we have no idea, so we just let tail --.
```java
class Solution {
    public int findMin(int[] nums) {
        if(nums == null || nums.length == 0) return -1;
        int min = nums[0];
        int head = 0, tail = nums.length - 1;
        while(head <= tail){
            int mid = head + (tail - head) / 2;
            min = Math.min(min, nums[mid]);
            if(nums[mid] == nums[head] && nums[mid] == nums[tail]) tail --;
            else if(nums[mid] > nums[tail]) head = mid + 1;
            else tail = mid;
        }
        return nums[head];
    }
}
```
