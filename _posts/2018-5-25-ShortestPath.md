---
layout: post
title: Shortest Path
---

## Undirected Unweighted Graph
### BFS solution
This is just like level traversal. For each level, get the size and then expand every node. The nodes on the same level have the same distance.

Here use HashSet, not Hashtable, because we only need to check whether it is in the set.
```java
/**
 * Definition for graph node.
 * class GraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x; neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */
public class Solution {
    /**
     * @param graph: a list of Undirected graph node
     * @param A: nodeA
     * @param B: nodeB
     * @return:  the length of the shortest path
     */
    public int shortestPath(List<UndirectedGraphNode> graph, UndirectedGraphNode A, UndirectedGraphNode B) {
        Queue<UndirectedGraphNode> q = new LinkedList<UndirectedGraphNode>();
        HashSet<UndirectedGraphNode> visited = new HashSet<UndirectedGraphNode>();
        q.offer(A);
        visited.add(A);
        int distance = 0;
        while(!q.isEmpty()){
            int size = q.size();
            for(int i = 0; i < size; i++){
                UndirectedGraphNode curr = q.poll();
                if(curr == B) return distance; 
                for(UndirectedGraphNode neighbor : curr.neighbors)
                    if(!visited.contains(neighbor)){
                        q.offer(neighbor);
                        visited.add(neighbor);
                    }
            }
            distance ++;
        }
        return -1;
    }
}
```

### Bidirectional BFS
```java
/**
 * Definition for graph node.
 * class GraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x; neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */
public class Solution {
    /**
     * @param graph: a list of Undirected graph node
     * @param A: nodeA
     * @param B: nodeB
     * @return:  the length of the shortest path
     */
    public int shortestPath(List<UndirectedGraphNode> graph, UndirectedGraphNode A, UndirectedGraphNode B) {
        Queue<UndirectedGraphNode> qstart = new LinkedList<UndirectedGraphNode>();
        HashSet<UndirectedGraphNode> visited_start = new HashSet<UndirectedGraphNode>();
        Queue<UndirectedGraphNode> qend = new LinkedList<UndirectedGraphNode>();
        HashSet<UndirectedGraphNode> visited_end = new HashSet<UndirectedGraphNode>();
        
        qstart.offer(A);
        qend.offer(B);
        visited_start.add(A);
        visited_end.add(B);
        int distance = 0;
        while(!qstart.isEmpty() && !qend.isEmpty()){
            int size = qstart.size();
            for(int i = 0; i < size; i++){
                UndirectedGraphNode curr = qstart.poll();
                if(visited_end.contains(curr)) return distance; 
                for(UndirectedGraphNode neighbor : curr.neighbors)
                    if(!visited_start.contains(neighbor)){
                        qstart.offer(neighbor);
                        visited_start.add(neighbor);
                    }
            }
            distance ++;
            size = qend.size();
            for(int i = 0; i < size; i++){
                UndirectedGraphNode curr = qend.poll();
                if(visited_start.contains(curr)) return distance; 
                for(UndirectedGraphNode neighbor : curr.neighbors)
                    if(!visited_end.contains(neighbor)){
                        qend.offer(neighbor);
                        visited_end.add(neighbor);
                    }
            }
            distance ++;
        }
        return -1;
    }
}
```

Start from start and end. When the node we want to expand is already visited in the other queue, we can return the distance. 
We can also move the return statement into the expand process, which is more clear. 
