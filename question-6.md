# 6. (Page: 6 | Coordinates: a1 - y31 | Points: 10.0 pts)

Write a Java function that receives a list of vertex pairs representing the edges of a graph. The program should determine the adjacency relationships and return the adjacency matrix. (Produce a version that works when loops, multiple edges, or directed edges are present.)  

```java
package adjacency;

import java.util.*;

public class AdjacencyMatrix {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Is the graph directed? (y/n): ");
        String directedInput = scanner.nextLine().trim();
        boolean isDirected = directedInput.equalsIgnoreCase("y");
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
        Set<String> vertexSet = new HashSet<>();
        for (String[] edge : edges) {
            vertexSet.add(edge[0]);
            vertexSet.add(edge[1]);
        }
        List<String> vertices = new ArrayList<>(vertexSet);
        Collections.sort(vertices);
        Map<String, Integer> vertexIndexMap = new HashMap<>();
        for (int i = 0; i < vertices.size(); i++) {
            vertexIndexMap.put(vertices.get(i), i);
        }
        int n = vertices.size();
        int[][] matrix = new int[n][n];
        for (String[] edge : edges) {
            String u = edge[0];
            String v = edge[1];
            int i = vertexIndexMap.get(u);
            int j = vertexIndexMap.get(v);
            if (isDirected) {
                matrix[i][j]++;
            } else {
                matrix[i][j]++;
                if (i != j) {
                    matrix[j][i]++;
                }
            }
        }
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```
