# Reconstruct Itinerary
## https://leetcode.com/problems/reconstruct-itinerary


# Implementation 1 : (Finding Euler Path)
Idea is to find the Euler path in a given graph, visiting each edge of the graph (ticket in this problem) exactly once.
```java
class Solution {
    public List<String> findItinerary(List<List<String>> tickets) {
        Map<String,PriorityQueue<String>> graph = new HashMap<>();
        for(List<String> ticket: tickets) {
            String u = ticket.get(0);
            String v = ticket.get(1);
            graph.putIfAbsent(u, new PriorityQueue<String>());
            graph.get(u).add(v);
        }
        
        List<String> result = new ArrayList<>();
        traverse("JFK", graph, result);
        return result;
    }
    
    private void traverse(String sourceVertex, Map<String,PriorityQueue<String>> graph, List<String> result) {
        PriorityQueue<String> neighbors = graph.get(sourceVertex);
        if(neighbors != null) {
            while(!neighbors.isEmpty()) {
                String v = neighbors.poll();
                traverse(v, graph, result);
            }
        }
        result.add(0,sourceVertex);
    }
}
```


# References :
https://www.youtube.com/watch?v=U33blOQRaJ0 (Hindi, Good explanation)

