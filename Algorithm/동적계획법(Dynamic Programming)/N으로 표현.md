# N으로 표현

[N으로 표현](https://school.programmers.co.kr/learn/courses/30/lessons/42895)

## 개념
+ 1~8을 key로 하는 ListSet 선언
+ 각 List는 HashSet으로 선언
  + dp.get(i)는 N을 i개 이용해서 만들 수 있는 숫자 
    + N을 i개 붙여쓴 수 추가
      + ex) 555
    + N을 i개 쪼개서 쓴 수 추가
      + ex) 5+5+5
      + 반복문 돌면서 j=1부터 시작해서 i까지 
        + dp.get(j) 반복문 돌면서 : a
          + dp.get(i-j)반복문 돌면서 : b
            + dp.get(i).add로 a랑 b 이용해서 할 수 있는 사칙연산 다 넣기 

    + number가 dp.get(i).contains(number)에 포함되는지 확인
    + 포함되면 return i 
+ 아니면 return -1
## 풀이
```java
import java.util.*;
import java.io.*; 

class Solution {
    public int solution(int N, int number) {
        if(N == number){
            return 1; 
        }
        
        List<Set<Integer>> dp = new ArrayList<>();
        
        for(int i=0; i <=8; i++){
            dp.add(new HashSet<>());
        }
        
        dp.get(1).add(N);
 
        for (int i = 2; i <= 8; i++){
            int concat=0;
            
            //붙여쓴 수
            for(int j=0; j<i; j++){
                concat = concat*10+N;
            }
            dp.get(i).add(concat);
            
            //쪼개서 사칙연산
            for(int j =1; j < i; j++){
                for(int a:dp.get(j)){
                    for(int b:dp.get(i-j)){
                        dp.get(i).add(a+b);
                        dp.get(i).add(a-b);
                        dp.get(i).add(b-a);
                        dp.get(i).add(a*b);
                        if(b!=0) dp.get(i).add(a/b);
                        if(a!=0) dp.get(i).add(b/a);
                    }
                }
            }
            if(dp.get(i).contains(number)) return i; 
        }
             
        return -1;
    }
}
```