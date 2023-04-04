# 9주차 코테 준비
## 4월 3일
### 1. 2장 Array(1, 2차원 배열) > 1번 큰 수 출력하기  
```java
import java.util.*;
class Main {	
	public ArrayList<Integer> solution(int n, int[] arr){
		ArrayList<Integer> answer = new ArrayList<>();
		answer.add(arr[0]);
		for(int i=1; i<n; i++){
			if(arr[i]>arr[i-1]) answer.add(arr[i]);
		}
		return answer;
	}

	public static void main(String[] args){
		Main T = new Main();
		Scanner kb = new Scanner(System.in);
		int n=kb.nextInt();
		int[] arr=new int[n];
		for(int i=0; i<n; i++){
			arr[i]=kb.nextInt();
		}
		for(int x : T.solution(n, arr)){
			System.out.print(x+" ");
		}
	}
}
```  
  1차원 ArrayList를 통해 단순 비교  

### 2. 6장 Sorting and Searching > 5번 중복확인  
```java
import java.util.*;
class Main {	
	public String solution(int n, int[] arr){
		String answer="U";
		Arrays.sort(arr);
		for(int i=0; i<n-1; i++){
			if(arr[i]==arr[i+1]){
				answer="D";
				break;
			}
		}
		return answer;
	}
	public static void main(String[] args){
		Main T = new Main();
		Scanner kb = new Scanner(System.in);
		int n=kb.nextInt();
		int[] arr=new int[n];
		for(int i=0; i<n; i++) arr[i]=kb.nextInt();
		System.out.println(T.solution(n, arr));
	}
}
```  
  hashmap이 제일 빠르지만(O(1)) 정렬로도 해결 가능하다. but O(nlgn)  
  Array.sort(배열명) --> 오름차순 정렬 후 n개 for문  

### 3. 6장 Sorting and Searching > 6번 장난꾸러기  
어떤 문제는 정렬을 하면 빨리 풀리기도 한다  
```java
import java.util.*;
class Main {	
	public ArrayList<Integer> solution(int n, int[] arr){
		ArrayList<Integer> answer=new ArrayList<>();
		int[] tmp=arr.clone();
		Arrays.sort(tmp);
		for(int i=0; i<n; i++){
			if(arr[i]!=tmp[i]) answer.add(i+1);
		}
		return answer;
	}
	public static void main(String[] args){
		Main T = new Main();
		Scanner kb = new Scanner(System.in);
		int n=kb.nextInt();
		int[] arr=new int[n];
		for(int i=0; i<n; i++) arr[i]=kb.nextInt();
		for(int x : T.solution(n, arr)) System.out.print(x+" ");
	}
}
```  
  tmp라는 배열에 깊은 복사로 오름차순으로 정렬.  
  arr과 tmp가 같지 않은 곳 찾기  

## 4월 4일  
### 1. 7장 Recursive, Tree, Graph(DFS, BFS 기초) > 1번 재귀함수  
```java
import java.util.*;
class Main {
	public void DFS(int n){
		if(n==0) return;
		else{
			DFS(n-1);
			System.out.print(n+" ");
		}
	}

	public void solution(int n){
		DFS(n);
	}
	public static void main(String[] args){
		Main T = new Main();
		T.solution(3);
		//System.out.println(T.solution(3));
	}	
}
```  
단순 for문으로 가능한 문제를 재귀로 해결  
 
### 2. 7장 Recursive, Tree, Graph(DFS, BFS 기초) > 2번 이진수 출력(재귀)  
10진수 N이 입력되면 2진수로 변환. 단, 재귀함수를 이용
```java
import java.util.*;
class Main {
	public void DFS(int n){
		if(n==0) return;
		else{
			DFS(n/2);
			System.out.print(n%2);
		}
	}

	public void solution(int n){
		DFS(n);
	}
	public static void main(String[] args){
		Main T = new Main();
		T.solution(11);
		//System.out.println(T.solution(3));
	}	
}
```  
return 찍힐 때까지 print문은 stack에 쌓인다  

### 3. 7장 Recursive, Tree, Graph(DFS, BFS 기초) > 3번 팩토리얼  
```java
import java.util.*;
class Main {
	public int DFS(int n){
		if(n==1) return 1;
		else return n*DFS(n-1);
	}
	public static void main(String[] args){
		Main T = new Main();
		System.out.println(T.DFS(5));
	}	
}
```  
피보나치 재귀랑 유사  

### 4. 7장 Recursive, Tree, Graph(DFS, BFS 기초) > 4번 피보나치 재귀  
```java
import java.util.*;
class Main {
	public int DFS(int n){
		if(n==1) return 1;
		else if(n==2) return 1;
		else return DFS(n-2)+DFS(n-1);
	}
	public static void main(String[] args){
		Main T = new Main();
		int n=10;
		for(int i=1; i<=n; i++) System.out.print(T.DFS(i)+" ");
	}	
}
```  
계속 같은 거 호출해서 굉장히 느림  

```java
import java.util.*;
class Main {
	static int[] fibo;
	public int DFS(int n){
		if(fibo[n]>0) return fibo[n];
		if(n==1) return fibo[n]=1;
		else if(n==2) return fibo[n]=1;
		else return fibo[n]=DFS(n-2)+DFS(n-1);
	}
	public static void main(String[] args){
		Main T = new Main();
		int n=45;
		fibo=new int[n+1];
		T.DFS(n);
		for(int i=1; i<=n; i++) System.out.print(fibo[i]+" ");
	}	
}
```  
메모이제이션으로 호출 수 줄어듦  

```java
public class Main {
	static int[] fibo;
	public int DFS(int n){
		if(fibo[n]>0) return fibo[n];
		else return fibo[n]=DFS(n-2)+DFS(n-1);
	}
	
	public static void main(String[] args){
        	Scanner in=new Scanner(System.in);
		int n = in.nextInt();
		Main T = new Main();
		
		fibo=new int[n+1];
		fibo[1] = 1; fibo[2] = 1;
		if (n!= 1 && n!= 2) {
			T.DFS(n);
		}
		for(int i=1; i<=n; i++) System.out.print(fibo[i]+" ");
	}	
}
```  
 함수 내에 조건문 두개 보기 싫어서 지워버림  
