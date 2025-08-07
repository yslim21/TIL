# K번째 수 

[K번째 수](https://www.acmicpc.net/problem/1300)

## k번째 수 
+ 이진 탐색을 이용하여 중앙값보다 작거나 같은 수가 몇개인지 구함 ->  그 개수가 K이상이면 정답 후보가 될 수 있음 
+ 범위를 점점 좁히면서 start가 > end가 됐을 떄의 정답후보가 결국 정답이되는것 

## 풀이
+ k번째 수는 k를 넘지 못함 -> 초기 end를 k로 설정해도됨 
```java
import java.io.*;
import java.util.*;

class Main{
    static int N,M;
    
    public static void main(String[] args)throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        N = Integer.parseInt(st.nextToken());
        
        st = new StringTokenizer(br.readLine());
        M = Integer.parseInt(st.nextToken());
        
        long start = 1;
        long end = (long)N*N; 
        long ans =0; 
        
        while(start <= end){
            long mid = (start+end)/2;
            
            long sum =0; 
            
            for(int i =1; i <=N; i++){
                sum += Math.min(N, mid/i);
            }
            
            if(sum < M){
                start = mid +1;
            }else{
                ans = mid;
                end = mid-1; 
            }
        }
        
        System.out.println(ans);
        
      
    }
}
```