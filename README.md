# Reconstruct Itinerary
## https://leetcode.com/problems/reconstruct-itinerary

You are given a list of airline tickets where tickets[i] = [fromi, toi] represent the departure and the arrival airports of one flight. Reconstruct the itinerary in order and return it.

All of the tickets belong to a man who departs from "JFK", thus, the itinerary must begin with "JFK". If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.

For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].
You may assume all tickets form at least one valid itinerary. You must use all the tickets once and only once.


# Implementation 1 : Finding Euler Path using DFS
Idea is to find the Euler path in a given graph, visiting **all the edges** of the graph (ticket in this problem) **exactly once.**
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

