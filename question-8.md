# 8. (Page: 8 | Coordinates: a1 - y31 | Points: 10.0 pts)

Write a Java function that receives two graphs represented by their sets of vertices and edges. The program should determine whether the two graphs are isomorphic or not and return the result.

```java
package isomorphism;
import java.util.*;
public class GI {
    public static void main(String[] a) {
        Scanner s = new Scanner(System.in);
        Set<String>[] vs = new Set[2];
        List<String[]>[] es = new List[2];
        int[] ec = new int[2];
        for (int i=0; i<2; i++) {
            System.out.println("G"+(i+1)+":");
            System.out.print("V: ");
            vs[i] = new HashSet<>(Arrays.asList(s.nextLine().split(" ")));
            System.out.print("E: ");
            ec[i] = s.nextInt(); s.nextLine();
            es[i] = new ArrayList<>();
            for (int j=0; j<ec[i]; j++) {
                System.out.print("E"+(j+1)+": ");
                String[] e = s.nextLine().split(" ");
                if (e.length != 2) { System.out.println("Retry."); j--; }
                else es[i].add(e);
            }
        }
        if (vs[0].size() != vs[1].size() || ec[0] != ec[1]) {
            System.out.println("Not isomorphic."); return; }
        Map<String,Integer>[] deg = new Map[2];
        for (int i=0; i<2; i++) {
            deg[i] = new HashMap<>();
            for (String v : vs[i]) deg[i].put(v,0);
            for (String[] e : es[i]) {
                String u=e[0], w=e[1];
                deg[i].put(u, deg[i].get(u) + (u.equals(w) ? 2 : 1));
                if (!u.equals(w)) deg[i].put(w, deg[i].get(w) + 1);
            }
        }
        List<Integer> d0 = new ArrayList<>(deg[0].values());
        List<Integer> d1 = new ArrayList<>(deg[1].values());
        Collections.sort(d0); Collections.sort(d1);
        if (!d0.equals(d1)) { System.out.println("Not isomorphic."); return; }
        List<String>[] sv = new List[2];
        int n = vs[0].size();
        for (int i=0; i<2; i++) {
            sv[i] = new ArrayList<>(vs[i]); Collections.sort(sv[i]);
        }
        int[][][] adj = new int[2][n][n];
        for (int g=0; g<2; g++)
            for (String[] e : es[g]) {
                int i = sv[g].indexOf(e[0]), j = sv[g].indexOf(e[1]);
                if (i==j) adj[g][i][i] = 1;
                else { adj[g][i][j] = 1; adj[g][j][i] = 1; }
            }
        List<List<Integer>> perms = permute(n);
        for (List<Integer> p : perms) {
            boolean match = true;
            for (int i=0; i<n && match; i++)
                for (int j=0; j<n; j++)
                    if (adj[0][i][j] != adj[1][p.get(i)][p.get(j)]) {
                        match = false; break; }
            if (match) { System.out.println("Isomorphic."); return; }
        }
        System.out.println("Not isomorphic.");
    }
    static List<List<Integer>> permute(int n) {
        List<List<Integer>> r = new ArrayList<>();
        bt(r, new ArrayList<>(), new boolean[n], n);
        return r;
    }
    static void bt(List<List<Integer>> r, List<Integer> t, boolean[] u, int n) {
        if (t.size() == n) r.add(new ArrayList<>(t));
        else for (int i=0; i<n; i++)
            if (!u[i]) {
                u[i] = true; t.add(i);
                bt(r, t, u, n);
                u[i] = false; t.remove(t.size()-1);
            }
    }
}
```
