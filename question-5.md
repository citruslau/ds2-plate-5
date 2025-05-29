# Write a Java function that receives a list of edges of a simple graph. The program should determine whether the graph is bipartite and return the result  

Write a Java function that receives a list of edges of a simple graph. The program should determine whether the graph is bipartite and return the result.  

```java
package bipartitegraph;

import java.util.*;

public class BipartiteGraph {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the number of edges: ");
        int numEdges = Integer.parseInt(scanner.nextLine().trim());
        List<String[]> edges = new ArrayList<>();
        for (int i = 0; i < numEdges; i++) {
            System.out.print("Enter edge " + (i + 1) + " (two space-separated vertices): ");
            String[] edge = scanner.nextLine().split("\\s+");
            if (edge.length != 2) {
                System.out.println("Invalid input. Please enter exactly two vertices per edge.");
                i--;
            } else {
                edges.add(edge);
            }
        }
        Map<String, List<String>> adjList = new HashMap<>();
        for (String[] edge : edges) {
            String u = edge[0];
            String v = edge[1];
            adjList.computeIfAbsent(u, k -> new ArrayList<>()).add(v);
            adjList.computeIfAbsent(v, k -> new ArrayList<>()).add(u);
        }
        Map<String, Integer> colorMap = new HashMap<>();
        boolean isBipartite = true;
        for (String node : adjList.keySet()) {
            if (!colorMap.containsKey(node)) {
                Queue<String> queue = new LinkedList<>();
                queue.add(node);
                colorMap.put(node, 0);
                while (!queue.isEmpty()) {
                    String current = queue.poll();
                    int currentColor = colorMap.get(current);
                    for (String neighbor : adjList.get(current)) {
                        if (!colorMap.containsKey(neighbor)) {
                            colorMap.put(neighbor, 1 - currentColor);
                            queue.add(neighbor);
                        } else if (colorMap.get(neighbor) == currentColor) {
                            isBipartite = false;
                            break;
                        }
                    }
                    if (!isBipartite) break;
                }
            }
            if (!isBipartite) break;
        }
        if (isBipartite) {
            System.out.println("The graph is bipartite.");
        } else {
            System.out.println("The graph is not bipartite.");
        }
    }
}
```
