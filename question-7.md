# 7. (Page: 7 | Coordinates: a1 - y31 | Points: 10.0 pts)

Write a Java function that receives vertex pairs and the number of times each edge appears in an undirected graph. The program should determine the incidence relationships and return the incidence matrix.  

```java
package incidencematrix;

import java.util.*;

public class IncidenceMatrix {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the no. of distinct edge records: ");
        int nRecords = scanner.nextInt();
        List<String[]> records = new ArrayList<>();
        Set<String> vertexSet = new HashSet<>();
        int totalEdges = 0;
        for (int i = 0; i < nRecords; i++) {
            System.out.print("Enter edge record " + (i + 1) + " (vertex1 vertex2 multiplicity): ");
            String u = scanner.next();
            String v = scanner.next();
            int m = scanner.nextInt();
            records.add(new String[]{u, v, String.valueOf(m)});
            vertexSet.add(u);
            vertexSet.add(v);
            totalEdges += m;
        }
        List<String> vertices = new ArrayList<>(vertexSet);
        Collections.sort(vertices);
        Map<String, Integer> vertexIndexMap = new HashMap<>();
        for (int i = 0; i < vertices.size(); i++) {
            vertexIndexMap.put(vertices.get(i), i);
        }
        int numVertices = vertices.size();
        int[][] matrix = new int[numVertices][totalEdges];
        int colIndex = 0;
        for (String[] rec : records) {
            String u = rec[0];
            String v = rec[1];
            int m = Integer.parseInt(rec[2]);
            int uIdx = vertexIndexMap.get(u);
            int vIdx = vertexIndexMap.get(v);
            for (int j = 0; j < m; j++) {
                if (u.equals(v)) {
                    matrix[uIdx][colIndex] = 2;
                } else {
                    matrix[uIdx][colIndex] = 1;
                    matrix[vIdx][colIndex] = 1;
                }
                colIndex++;
            }
        }
        for (int i = 0; i < numVertices; i++) {
            for (int j = 0; j < totalEdges; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```
