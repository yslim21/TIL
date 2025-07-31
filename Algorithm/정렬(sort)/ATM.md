# ATM
[ATM](https://www.acmicpc.net/problem/11399)

## 개념
+ 인출 시간이 가장 적게 걸리는 사람 순으로 정렬
+ 합 배열을 이용하여 각 사람마다 기다리는 시간 구한후, 기다리는 시간 모두 합쳐서 출력
+ 삽입 정렬 이용
  + 2~마지막 위치까지 반복문 돌면서 현재 index에 있는 데이터 값을 1~현재-1 index에 있는 데이터값들과 비교하며 적절한 위치에 삽입 
 
## 풀이
```java
import java.util.*;
import java.io.*;

class Main{
    public static int N;
    public static void main(String[] args) throws IOException{
        
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        
        N = Integer.parseInt(st.nextToken());
        
        int[] arr = new int[N];
        int[] s = new int[N]; //합배열 
        
        st = new StringTokenizer(br.readLine(), " ");
        for(int i=0; i <N; i++){
            arr[i] = Integer.parseInt(st.nextToken());
        }
        
        for(int i=1; i <N; i++){
            int insert_point = i;
            int insert_value = arr[i];
            for(int j= i-1; j >= 0; j--){
                if(arr[j] < arr[i]){
                    insert_point = j+1;
                    break;
                }
                if(j==0){
                    insert_point = 0;
                }
            }
            
            for (int j = i; j > insert_point; j--) {
                arr[j] = arr[j - 1];
            }
            arr[insert_point] = insert_value; 
        }
        
        s[0] = arr[0];
        for(int i =1; i < N; i++){
            s[i] = s[i-1] + arr[i]; 
        }
        
        int sum =0;
        for(int i =0; i < N; i++){
            sum += s[i]; 
        }
        
        System.out.println(sum);
           
    }
}
```