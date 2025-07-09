# ABCDE

[ABCDE](https://www.acmicpc.net/problem/13023)

## 개념
+ 연결된 노드 graph에 저장(처음엔 2차원 배열에 저장했으나 시간 초과발생하여 수정함 )
+ 각각의 노드에서 시작 
  + dfs 이용해서 연결된 친구 호출 
  + 4명 이상 연결되어있으면 return true
  + 


## 풀이

```java
import java.util.*;
import java.io.*;

public class Main {
    static ArrayList<Integer>[] graph;
    static boolean[] visited;
    static int N, M;
    static boolean found = false;

    public static void DFS(int node, int depth) {
        if (found) return; // 이미 찾았으면 더 안 함

        if (depth == 4) {
            found = true;
            return;
        }

        for (int next : graph[node]) {
            if (!visited[next]) {
                visited[next] = true;
                DFS(next, depth + 1);
                visited[next] = false; // 백트래킹
            }
        }
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        graph = new ArrayList[N];
        for (int i = 0; i < N; i++) graph[i] = new ArrayList<>();

        for (int i = 0; i < M; i++) {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());

            graph[u].add(v);
            graph[v].add(u);
        }

        visited = new boolean[N];

        for (int i = 0; i < N; i++) {
            visited[i] = true;
            DFS(i, 0);
            visited[i] = false;
            if (found) break;
        }

        System.out.println(found ? "1" : "0");
    }
}
```