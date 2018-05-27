---
layout: post
title: Hashmap and Heap
---
## Top k frequent elements

Pay attention to the use of Hashmap, Map.Entry in entrySet(), and how to overwrite the PriorityQueue. 
```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> count = new HashMap<Integer, Integer>();   // attention
        for(int num : nums){
            if(count.containsKey(num))
                count.put(num, count.get(num) + 1);
            else count.put(num, 1);
        }
        PriorityQueue<Map.Entry<Integer, Integer>> Max_heap = new PriorityQueue<>((a,b) -> (b.getValue() - a.getValue()));
        for(Map.Entry<Integer, Integer> entry : count.entrySet()){
            Max_heap.add(entry);
        }
        List<Integer> result = new ArrayList<Integer>();
        for(int i = 0; i < k; i ++){
            result.add(Max_heap.poll().getKey());
        }
        return result;
    }
}
```
