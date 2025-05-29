# 8. (Page: 8 | Coordinates: a1 - y31 | Points: 10.0 pts)

Write a Java function that receives two graphs represented by their sets of vertices and edges. The program should determine whether the two graphs are isomorphic or not and return the result.

```java
package isomorphism;

import java.util.*;

public class GraphIsomorphism {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("For graph1:");
        System.out.print("Enter vertices (space separated): ");
        String[] v1Tokens = scanner.nextLine().split("\\s+");
        Set<String> vertexSet1 = new HashSet<>(Arrays.asList(v1Tokens));
        System.out.print("Enter the number of edges: ");
        int e1 = scanner.nextInt();
        scanner.nextLine();
        List<String[]> edges1 = new ArrayList<>();
        for (int i = 0; i < e1; i++) {
            System.out.print("Enter edge " + (i + 1) + " (two vertices): ");
            String[] edgeTokens = scanner.nextLine().split("\\s+");
            if (edgeTokens.length != 2) {
                System.out.println("Invalid edge. Please enter two vertices.");
                i--;
            } else {
                edges1.add(edgeTokens);
            }
        }
        System.out.println("For graph2:");
        System.out.print("Enter vertices (space separated): ");
        String[] v2Tokens = scanner.nextLine().split("\\s+");
        Set<String> vertexSet2 = new HashSet<>(Arrays.asList(v2Tokens));
        System.out.print("Enter the number of edges: ");
        int e2 = scanner.nextInt();
        scanner.nextLine();
        List<String[]> edges2 = new ArrayList<>();
        for (int i = 0; i < e2; i++) {
            System.out.print("Enter edge " + (i + 1) + " (two vertices): ");
            String[] edgeTokens = scanner.nextLine().split("\\s+");
            if (edgeTokens.length != 2) {
                System.out.println("Invalid edge. Please enter two vertices.");
                i--;
            } else {
                edges2.add(edgeTokens);
            }
        }
        if (vertexSet1.size() != vertexSet2.size() || e1 != e2) {
            System.out.println("The graphs are not isomorphic.");
            return;
        }
        Map<String, Integer> degMap1 = new HashMap<>();
        for (String v : vertexSet1) {
            degMap1.put(v, 0);
        }
        for (String[] edge : edges1) {
            String u = edge[0];
            String v = edge[1];
            if (u.equals(v)) {
                degMap1.put(u, degMap1.get(u) + 2);
            } else {
                degMap1.put(u, degMap1.get(u) + 1);
                degMap1.put(v, degMap1.get(v) + 1);
            }
        }
        Map<String, Integer> degMap2 = new HashMap<>();
        for (String v : vertexSet2) {
            degMap2.put(v, 0);
        }
        for (String[] edge : edges2) {
            String u = edge[0];
            String v = edge[1];
            if (u.equals(v)) {
                degMap2.put(u, degMap2.get(u) + 2);
            } else {
                degMap2.put(u, degMap2.get(u) + 1);
                degMap2.put(v, degMap2.get(v) + 1);
            }
        }
        List<Integer> degSeq1 = new ArrayList<>(degMap1.values());
        List<Integer> degSeq2 = new ArrayList<>(degMap2.values());
        Collections.sort(degSeq1);
        Collections.sort(degSeq2);
        if (!degSeq1.equals(degSeq2)) {
            System.out.println("The graphs are not isomorphic.");
            return;
        }
        List<String> vertices1 = new ArrayList<>(vertexSet1);
        Collections.sort(vertices1);
        List<String> vertices2 = new ArrayList<>(vertexSet2);
        Collections.sort(vertices2);
        int n = vertices1.size();
        int[][] adj1 = new int[n][n];
        for (String[] edge : edges1) {
            String u = edge[0];
            String v = edge[1];
            int i = vertices1.indexOf(u);
            int j = vertices1.indexOf(v);
            if (i == j) {
                adj1[i][i] = 1;
            } else {
                adj1[i][j] = 1;
                adj1[j][i] = 1;
            }
        }
        int[][] adj2 = new int[n][n];
        for (String[] edge : edges2) {
            String u = edge[0];
            String v = edge[1];
            int i = vertices2.indexOf(u);
            int j = vertices2.indexOf(v);
            if (i == j) {
                adj2[i][i] = 1;
            } else {
                adj2[i][j] = 1;
                adj2[j][i] = 1;
            }
        }
        List<Integer> indices = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            indices.add(i);
        }
        List<List<Integer>> perms = generatePermutations(indices);
        for (List<Integer> p : perms) {
            boolean match = true;
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (adj1[i][j] != adj2[p.get(i)][p.get(j)]) {
                        match = false;
                        break;
                    }
                }
                if (!match) break;
            }
            if (match) {
                System.out.println("The graphs are isomorphic.");
                return;
            }
        }
        System.out.println("The graphs are not isomorphic.");
    }

    private static List<List<Integer>> generatePermutations(List<Integer> list) {
        List<List<Integer>> result = new ArrayList<>();
        if (list.isEmpty()) {
            result.add(new ArrayList<>());
            return result;
        }
        boolean[] used = new boolean[list.size()];
        backtrack(result, new ArrayList<>(), used, list);
        return result;
    }

    private static void backtrack(List<List<Integer>> result, List<Integer> temp, boolean[] used, List<Integer> list) {
        if (temp.size() == list.size()) {
            result.add(new ArrayList<>(temp));
            return;
        }
        for (int i = 0; i < list.size(); i++) {
            if (!used[i]) {
                used[i] = true;
                temp.add(list.get(i));
                backtrack(result, temp, used, list);
                temp.remove(temp.size() - 1);
                used[i] = false;
            }
        }
    }
}
```
