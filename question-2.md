# 2. (Page: 2 | Coordinates: a1 - y31 | Points: 10.0 pts)

Write a Java function that receives an adjacency matrix of a graph. The program should determine the list of edges in the graph and return the number of times each edge appears.  

```java
package graphedges;

import java.util.Scanner;

public class GraphEdges {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Is the graph directed? (y/n): ");
        String directedInput = scanner.nextLine().trim();
        boolean isDirected = directedInput.equalsIgnoreCase("y");
        System.out.print("Enter the number of vertices: ");
        int n = scanner.nextInt();
        int[][] matrix = new int[n][n];
        System.out.println("Enter the adjacency matrix row by row (each row in one line, space separated):");
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }
        if (isDirected) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (i != j && matrix[i][j] > 0) {
                        System.out.println("Edge " + i + " -> " + j + ": " + matrix[i][j] + " time(s)");
                    }
                }
            }
        } else {
            for (int i = 0; i < n; i++) {
                for (int j = i + 1; j < n; j++) {
                    if (matrix[i][j] > 0) {
                        System.out.println("Edge " + i + " - " + j + ": " + matrix[i][j] + " time(s)");
                    }
                }
            }
        }
    }
}
```
