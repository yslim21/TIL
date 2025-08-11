# GCDNK1
[GCDNK1](https://www.acmicpc.net/problem/11689)

## 개념
+ 오일러 피 이용 

## 풀이1 - 오답
+ 배열의 길이나 인덱스는 int만 가능 
```java
import java.io.*;
import java.util.*;

class Main{
    public static void main(String[] args)throws IOException{
        Scanner in = new Scanner(System.in);
        long N= in.nextLong();
        long[] A = new long[N+1];
        
        for(long i=1; i <= N; i++){
            A[i] = i;
        }
        
        for(long i =2; i <=N; i++){
            if(A[i] == N){
                for(long j =i; i<=N; j= j+i){
                    A[j] = A[j]-A[j]/2;
                }
            }
        }
        
        System.out.println(A[N]);
    }
}
```

## 풀이2
+ phi[N] 하나만 구하자 
+ 루프 종료 조건이 i^2 <=N인데 N는 더 이상 작은 인수를 가지지 않는 소수임
+ 그래서 마지막에 N를 한 번 더 반영하는 if (N> 1)이 필요합
```java
import java.io.*;
import java.util.*;

class Main{
    public static void main(String[] args)throws IOException{
        Scanner in = new Scanner(System.in);
        long N= in.nextLong();
        long result = N; 
        
        for(long i =2; i <=Math.sqrt(N); i++){
            if(N % i == 0){
                result = result - result/i;
                while(N%i ==0){
                    N /= i;
                }
            }
        }
        
        if(N>1){
            result = result - result/N;
        } // 반복문에서 제곱근까지만 탐색했으므로 1개의 소인수가 누락되는 케이스 
        
        System.out.println(result);
    }
}
```