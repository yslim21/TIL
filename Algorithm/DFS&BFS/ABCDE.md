# ABCDE

[ABCDE](https://www.acmicpc.net/problem/13023)

## 개념
+ DFS 이용
+ depth가 5이상이면 조건 만족한 것 -> DFS를 이용해서 depth가 5이상인지 검사
+ 0,1,2,~N-1 즉, 모든 노드를 기준으로 DFS를 해야하므로 한번의 탐색이 끝나면 해당 노드 방문 상태를 false로 변경해야함

## 풀이
```java
import java.util.*;
import java.io.*;

class Main{
    public static int N,M;
    public static ArrayList<Integer>[] A;
    public static boolean visited[];
    public static int depth;
    public static boolean arrive; 
    
    public static void main(String[] args) throws IOException{
        
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        
        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());
        
        A = new ArrayList[N];
        visited = new boolean[N];
        
        for(int i=0; i < N; i++){
            A[i] = new ArrayList<Integer>();
        }
         
        for(int i=0; i < M; i++){
            st = new StringTokenizer(br.readLine(), " ");
            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            A[s].add(e);
            A[e].add(s);
        }
        depth = 1;
        for(int i=0; i < N; i++){
            DFS(i,depth);
            if(arrive){
                break;
            }
        }
        if(arrive){
            System.out.println("1");
        }else
           System.out.println("0"); 
        
        
        
        
    }
    
    static void DFS(int v, int depth){
        if(depth == 5 || arrive){
            arrive = true; 
            return; 
        }
        
        visited[v] = true;
        
        for(int i : A[v]){
            if(!visited[i]){
                DFS(i,depth+1);
            }
        }
        
        visited[v] = false;
        
    }
}
```