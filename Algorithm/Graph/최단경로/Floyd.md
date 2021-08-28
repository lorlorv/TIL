# Floyd 🗺
: 모든 정점 사이의 최단 경로를 찾는다. </br>
: 2차원 배열 A를 사용하여 3중 반복을 하는 루프로 구성되어있다.

---

## 알고리즘 
```JAVA
floyd(G) :
    for k ← 0 to n - 1
        for i ← 0 to n - 1
            for j ← 0 to n - 1
                A[i][j] = min(A[i][j], A[i][k] + A[k][j])
```
---

### A^k[i][j]
: 0부터 k까지의 정점만을 이용한 정점 i에서 정점 j까지의 최단 경로 길이

---

### 구하려는 답
: Aⁿ­-¹ [i][j] </br>
→ 0부터 n-1까지의 모든 정점을 이용한 최단 경로

---

### Floyd 알고리즘의 핵심적인 내용 
: A-¹ → A^0 → … Aⁿ-¹ 순으로 최단 거리를 구하자는 것! </br>
: A-¹ == weight 배열의 값

---

### if ) A^(k - 1) 까지 구해진 상태에서 k번째 정점이 추가로 고려되는 상황
![](/Images/floyd개념.JPG) </br>
⇒ 0부터 k까지의 정점만을 사용하여 정점 i에서 정점 j로 가는 2가지의 최단 경로 경우 

1. **정점 k를 거쳐서 가지 않는 경우** 
    - A^k[i][j]는 k보다 큰 정점은 통과하지 않으므로 최단 거리는 여전히 A^(k-1)[i][j]이다.
2. **정점 k를 거치는 경우**
    - i에서 k까지의 최단거리 A^(k-1)[i][k]에 k에서 j까지의 최단거리 A^(k-1)[k][j]를 더한 값.

### ∴ 최종적인 최단거리 
- A^(k-1)[i][k]와 A^(k-1)[i][k] + A^(k-1)[k][j] 중 보다 적은 값이 A^k[i][j]가 된다.
- 정점 k를 경유하는 것이 보다 좋은 경로이면 A^(k-1)[i][j]값이 변경되고 그렇지 않으면, 이전 값을 유지한다.
---

### 👀 EX
![](/Images/floyd그림.JPG)
0|1|2|3|4|5|6
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
0|7|∞|∞|3|10|∞|
7|0|4|10|2|6|∞|
∞|4|0|2|∞|∞|∞|
∞|10|2|0|11|9|4|
3|2|∞|11|0|∞|5|
10|6|∞|9|∞|0|∞|
∞|∞|∞|4|5|∞|0|

<정점 0을 거쳐서 가는 경로와 비교하여 최단거리를 수정> </br>
A^0[i][j] = min (A-¹[i][j], A-¹[i][0] + A-¹[0][j])
- i == 4 && j == 5
- ∞ > **3 + 10**

0|1|2|3|4|5|6
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
0|7|∞|∞|3|10|∞|
7|0|4|10|2|6|∞|
∞|4|0|2|∞|∞|∞|
∞|10|2|0|11|9|4|
3|2|∞|11|0|**13**|5|
10|6|∞|9|**13**|0|∞|
∞|∞|∞|4|5|∞|0|

<정점 1을 거쳐서 가는 경로와 비교하여 최단거리를 수정> </br>
A¹[i][j] = min (A^0[i][j], A^0[i][1] + A^0[1][j])

0|1|2|3|4|5|6
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
0|7|**11**|**17**|3|10|∞|
7|0|4|10|2|6|∞|
**11**|4|0|2|**6**|**10**|∞|
**17**|10|2|0|11|9|4|
3|2|**6**|11|0|**8**|5|
10|6|**10**|9|**8**|0|∞|
∞|∞|∞|4|5|∞|0|

---

## 복잡도
: 네트워크에 n개의 정점이 있다면, 3중 반복문이 실행되므로 
- `시간복잡도` : O(n³)
- `공간복잡도` : O(n²)

---

## 풀이 시 주의사항 
: INF ← Integer.MAX_VALUE (❌)
- 나중에 가중치 합할 때 ∞ + 자연수 </br>⇒ **Overflow**로 인해 음수가 되기 때문!

---

## Dijkstra VS FLoyd
`Dijkstra `
1. 어떠한 정점을 기준으로 잡고 다른 모든 정점으로의 최단 거리를 구하는 알고리즘
2. 가장 적은 비용을 가지는 간선을 하나씩 선택하여 수행
3. 그리디 기법 기반

`Floyd`
1. 모든 정점에서 모든 정점으로의 최단 거리를 구하는 알고리즘 
2. 거쳐가는 정점을 기준으로 수행
3. 다이나믹 프로그래밍 기반

---

## 💻 코드 (BOJ 11404)
```Java
import java.io.*;

public class BOJ_11404 {
	static int n, m;
	static int a, b, c;
	static int[][] maps;
	static int INF = 10000001;

	public static void main(String[] args) throws IOException {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		n = Integer.parseInt(br.readLine());
		m = Integer.parseInt(br.readLine());
		
		//초기화
		maps = new int[n + 1][n + 1];
		for(int i = 1; i <= n; i++) {
			for(int j = 1; j <= n; j++) {
				maps[i][j] = INF;
				if(i == j)
					maps[i][j] = 0;					
			}
		}
		
		//입력
		for(int i = 0; i < m; i++) {
			String[] temp = br.readLine().split(" ");
			a = Integer.parseInt(temp[0]);
			b = Integer.parseInt(temp[1]);
			c = Integer.parseInt(temp[2]);
			//1 4 1 과 1 4 2가 들어왔을 때 1 4 1을 택해야하기 때문에 Math.min 사용
			maps[a][b] = Math.min(maps[a][b], c); 	
		}

		//floyd 함수
		floyd();
		
		//출력
		for(int i = 1; i <= n; i++) {
			for(int j = 1; j <= n; j++) {
				if(maps[i][j] == INF) //i에서 j로 갈 수 없는 경우 == floyd를 해도 비용이 INF인 경우
					bw.write("0 ");
				else
					bw.write(String.valueOf(maps[i][j]) + " " );
			}
			bw.newLine();
		}
		
		bw.flush();
		bw.close();
		
	}
	static void floyd() {
		for(int k = 1; k <= n; k++) {
			for(int i = 1; i <= n; i++) {
				for(int j = 1; j <= n; j++) {
					if(maps[i][j] > maps[i][k] + maps[k][j]) {
						maps[i][j] = maps[i][k] + maps[k][j];
					}
				}
			}
		}
				
	}	
}
```