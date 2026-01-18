# A와 B 2

[A와 B 2](https://www.acmicpc.net/problem/12919)

## 개념1 
+ dfs 이용해서 모든 문자 조합 탐색 
+ 문자열의 길이가 T와 같아지만 문자열과 T가 같은지 검사하고 맞으면 1 틀리면 0 출력

## 풀이1 - 오답 
+ 시간 복잡도가 2^(T길이-S길이)이므로 시간 초과 
```java
import java.io.*;

class Main{
    static String S, T;
    static int answer = 0; 

    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        S = br.readLine().trim();
        T = br.readLine().trim();

        dfs(S);

        System.out.println(answer);

        
    }

    static void dfs(String s){
        if(s.length() == T.length()){
            if (s.equals(T)) answer = 1;
            return;
        }

        dfs(new StringBuilder(s).append('A').toString());
        dfs(new StringBuilder(s).append('B').reverse().toString());
    }
}
```

## 개념2 
+ dfs를 이용하는데 T->S로 가면서 탐색 
+ 문자열이 A로 끝나면: 마지막 A 제거
+ 문자열이 B로 끝나면: 마지막 B 제거 후 reverse 

## 풀이2 
```java
import java.io.*;

class Main {
    static String S,T;
    static int answer = 0;

    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        S = br.readLine().trim();
        T = br.readLine().trim();

        dfs(T);
        System.out.println(answer);
    }

    static void dfs(String t) {
        if (t.length() == S.length()) {
            if (t.equals(S)) answer = 1;
            return;
        }

        //A로 끝나는 경우 
        if (t.endsWith("A")) {
            dfs(t.substring(0, t.length()-1));

        } 

        //B로 끝나서 revers한 경우 - 이때 else로 처리하면 A로 끝나고 B로 시작하는 경우 중 하나만 선택하게 되므로 둘다 탐색하기 위해서는 if문 처리 
        if(t.startsWith("B")){ 
            dfs(new StringBuilder(t.substring(1)).reverse().toString());

        }
    }
}
```