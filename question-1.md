# 1. (Page: 1 | Coordinates: a1 - y31 | Points: 10.0 pts)

Write a java function that receives a parameter of list of edges of a simple graph, the program should return and determine whether it is connected and return the number of connected components if it is not connected.  

```java
import java.util.*;

public class GraphConnectivity {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the number of edges: ");
        int n = scanner.nextInt();
        scanner.nextLine();
        List<String[]> edges = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            System.out.print("Enter edge " + (i + 1) + " (two space-separated vertices): ");
            String[] edge = scanner.nextLine().split("\\s+");
            if (edge.length != 2) {
                System.out.println("Invalid input. Please enter exactly two vertices.");
                i--;
            } else {
                edges.add(edge);
            }
        }
        int components = countConnectedComponents(edges);
        if (components == 1) {
            System.out.println("The graph is connected.");
        } else {
            System.out.println("The graph is not connected and has " + components + " connected components.");
        }
    }

    public static int countConnectedComponents(List<String[]> edges) {
        Set<String> vertices = new HashSet<>();
        Map<String, List<String>> adjList = new HashMap<>();
        for (String[] edge : edges) {
            String u = edge[0];
            String v = edge[1];
            vertices.add(u);
            vertices.add(v);
            adjList.computeIfAbsent(u, k -> new ArrayList<>()).add(v);
            adjList.computeIfAbsent(v, k -> new ArrayList<>()).add(u);
        }
        Set<String> visited = new HashSet<>();
        int components = 0;
        for (String node : vertices) {
            if (!visited.contains(node)) {
                components++;
                Queue<String> queue = new LinkedList<>();
                queue.add(node);
                visited.add(node);
                while (!queue.isEmpty()) {
                    String current = queue.poll();
                    for (String neighbor : adjList.getOrDefault(current, Collections.emptyList())) {
                        if (!visited.contains(neighbor)) {
                            visited.add(neighbor);
                            queue.add(neighbor);
                        }
                    }
                }
            }
        }
        return components;
    }
}
```
