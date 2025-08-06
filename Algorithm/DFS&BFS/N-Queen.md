# N-Queen

[N-Queen](https://www.acmicpc.net/problem/9663)

## 개념
+ DFS 이용
+ 2차원배열을 이용하지 않고 1차원 배열을 이용하여 인덱스는 행,값을 열이라고 보자
+ 퀸끼리 공격하지 않으려면 한 행당 한개의 퀸만 들어갈 수 있음
+ 대각선에 퀸이 존재하는 경우도 검사해야하는데, 인덱스 차이만큼 값도 차이가 나면 같은 대각선에 존재한다고 볼 수 있음 

## 풀이
```java
import java.util.*;
import java.io.*; 

class Main{
    public static int N,count;
    public static int[] A;
    
    public static void main(String[] args) throws IOException{
        
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        
        N = Integer.parseInt(st.nextToken());
        count = 0;
        
        A = new int[N];
        
        backTracking(0);
        System.out.println(count);
        
        
        
    }
    
    static void backTracking(int row){
        
        if(row == N){
            count++;
            return;
        }
        
        for(int i=0; i < N; i++){
            A[row] = i;
            if(check(row)){
                backTracking(row+1);
            }
        }            
    }
    
    static boolean check(int row){
        for(int i=0; i < row; i++){
            if(A[row] == A[i]){
                return false; 
            }
            if(Math.abs(row -i) == Math.abs(A[i] - A[row])){
                return false;
            }
        }
        return true;
    }
}
```