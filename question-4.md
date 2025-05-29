# 4. (Page: 4 | Coordinates: a1 - y31 | Points: 10.0 pts)

Write a Java function that receives a list of vertex pairs representing the edges of an undirected graph. The program should determine the degree of each vertex and return the result.  

```java
package vertexdegree;

import java.util.*;

public class VertexDegree {
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
        Map<String, Integer> degreeMap = new HashMap<>();
        for (String[] edge : edges) {
            String u = edge[0];
            String v = edge[1];
            if (u.equals(v)) {
                degreeMap.put(u, degreeMap.getOrDefault(u, 0) + 2);
            } else {
                degreeMap.put(u, degreeMap.getOrDefault(u, 0) + 1);
                degreeMap.put(v, degreeMap.getOrDefault(v, 0) + 1);
            }
        }
        List<String> vertices = new ArrayList<>(degreeMap.keySet());
        Collections.sort(vertices);
        for (String vertex : vertices) {
            System.out.println("Vertex " + vertex + " has degree " + degreeMap.get(vertex));
        }
    }
}
```
