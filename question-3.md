# 3. (Page: 3 | Coordinates: a1 - y31 | Points: 10.0 pts)

Write a Java function that receives a graph as input. The program should determine whether the graph contains a cycle or not and return the result.  

```java
package cycledetection;

import java.util.*;

public class CycleDetection {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the number of vertices: ");
        int n = scanner.nextInt();
        System.out.print("Enter the number of edges: ");
        int m = scanner.nextInt();
        List<Integer>[] adjList = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            adjList[i] = new ArrayList<>();
        }
        System.out.println("Enter the edges (each as two space-separated integers):");
        for (int i = 0; i < m; i++) {
            int u = scanner.nextInt();
            int v = scanner.nextInt();
            adjList[u].add(v);
            adjList[v].add(u);
        }
        boolean[] visited = new boolean[n];
        boolean hasCycle = false;
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                if (dfs(i, -1, visited, adjList)) {
                    hasCycle = true;
                    break;
                }
            }
        }
        if (hasCycle) {
            System.out.println("The graph contains a cycle.");
        } else {
            System.out.println("The graph does not contain a cycle.");
        }
    }

    private static boolean dfs(int node, int parent, boolean[] visited, List<Integer>[] adjList) {
        visited[node] = true;
        for (int neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                if (dfs(neighbor, node, visited, adjList)) {
                    return true;
                }
            } else if (neighbor != parent) {
                return true;
            }
        }
        return false;
    }
}
```
