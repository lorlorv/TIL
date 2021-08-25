# 최단경로
### 네트워크에서 정점 u와 정점 v를 연결하는 경로 중에서 간선들의 가중치 합이 최소가 되는 경로

### `최단 경로 알고리즘`
- [Dijkstra](#Dijkstra) : 하나의 시작 정점에서 다른 정점까지의 최단 경로 계산 
- [Floyd](#Floyd) : 모든 정점에서 다른 모든 정점까지의 최단 경로를 계산 

---
## Dijkstra
: 하나의 시작 정점으로부터 모든 다른 정점까지의 최단 경로 찾음 
### - `check[]` : 시작 정점 v로부터의 최단 경로가 이미 발견된 정점들의 집합
### - `distance[]` : 최단 경로가 알려진 정점들만을 이용한 다른 정점들까지의 최단 경로 길이 
- 매 단계에서 가장 distance값이 작은 정점을 check
- 새로운 정점이 check 되면 distance값 갱신
    - 새로 추가된 정점을 거쳐서 정점까지 가는 거리와 기존의 거리를 비교하여 더 작은 거리로 distance를 수정 
        ```Java
        distance[w] = min(distance[w], distance[u] + weight[u][w])
        ```

### -
![](/Images/Dijkstra.JPG)

## 💻배열로 구현한 코드
<details markdown = "1">
<summary>코드</summary>

```Java
//Dijkstra skeleton
package dijkstra;
class Graph{
	private int n; //노드들의 수 
	private int maps[][]; //노드들의 가중치 저장
	
	public Graph(int n) {
		this.n = n;
		maps = new int[n + 1][n + 1];
		
		//인접행렬 초기화
		for(int i=1; i<=n; ++i){
			for(int j=1; j<=n; ++j){
				maps[i][j] = Integer.MAX_VALUE; 
			} 			
		}		
	}
	
	public void input(int i, int j, int w) {
		maps[i][j] = w;
		maps[j][i] = w;
	}
	
	public void dijkstra(int v) {
		boolean check[] = new boolean[n + 1];
		int distance[] = new int[n + 1];
		
		for(int i = 1; i <= n; i++) {
			distance[i] = Integer.MAX_VALUE; //distance값 초기화
		}
		
		//시작노드 초기화!
		distance[v] = 0;
		check[v] = true;
		
		//정점에 인접해있고 방문하지 않은 정점 거리 갱신
		for(int i = 1; i <= n; i++) {
			if(!check[i] && maps[v][i] != Integer.MAX_VALUE) {
				distance[i] = maps[v][i];
			}
		}
		
		//모든 정점이 check배열에 들어갈 때 까지 
		for(int i = 0; i < n - 1; i++) {
			
			//최소 distance 찾기
			int min = Integer.MAX_VALUE;
			int index = -1;
			
			for(int j = 1; j <= n; j++) {
				if(!check[j]) {
					if(distance[j] < min) {
						min = distance[j];
						index = j;
					}
				}
			}
			
			check[index] = true;		
			//distance 갱신
			for(int j = 1; j <= n; j++) {
				if(!check[j] && maps[index][j] != Integer.MAX_VALUE) {
					if(distance[j] > distance[index] + maps[index][j]) {
						distance[j] = distance[index] + maps[index][j];
					}
				}
			}
			
		}
		
		for(int i = 1; i <= n; i++) {
			System.out.println(i + "번 노드까지 가는 최단 거리  : " + distance[i] + " ");
		}
	}
}
public class Dijkstra {

	public static void main(String[] args) {
		 Graph g = new Graph(5);
	        g.input(1, 2, 10);
	        g.input(1, 4, 60);
	        g.input(2, 4, 30);
	        g.input(2, 3, 45);
	        g.input(2, 5, 60);
	        g.input(3, 5, 20);
	        g.input(3, 4, 5);
	        g.dijkstra(1);
		 
	}

}

```
</details>


## 💻우선순위 큐로 구현한 코드
<details markdown = "1">
<summary>코드</summary>

```Java
package dijkstra_pq;

import java.util.PriorityQueue;

public class Dijkstra_pq {

	public static void main(String[] args) {
		Graph g = new Graph(5);
        g.input(1, 2, 10);
        g.input(1, 4, 60);
        g.input(2, 4, 30);
        g.input(2, 3, 45);
        g.input(2, 5, 60);
        g.input(3, 5, 20);
        g.input(3, 4, 5);
        g.dijkstra_pq(1);
	}
}

class Graph{
	private int n; //노드들의 수 
	private int maps[][]; //노드들의 가중치 저장
	
	class Node implements Comparable<Node>{
		private int weight;
		private int index; 
		
		public Node(int weight, int index) {
			this.weight = weight;
			this.index = index;
		}
	
		@Override
		public int compareTo(Node node) {
			return Integer.compare(this.weight, node.weight);
		}
		
	}
	
	//생성자
	public Graph(int n) { //초기화 역할
		this.n = n;
		maps = new int[n + 1][n + 1];
		
		//인접행렬 초기화
		for(int i=1; i<=n; ++i){
			for(int j=1; j<=n; ++j){
				maps[i][j] = Integer.MAX_VALUE; 
			} 			
		}		
	}
	
	public void input(int i, int j, int w) {
		maps[i][j] = w;
		maps[j][i] = w;
	}
	
		
	public void dijkstra_pq(int v) {
		PriorityQueue<Node> pq = new PriorityQueue<>();
		int distance[] = new int[n + 1];
		boolean check[] = new boolean[n + 1];
		
		//distance 초기화
		for(int i = 1; i <= n; i++) {
			distance[i] = Integer.MAX_VALUE;
		}
		//우선순위 큐에 start 정점과 index를 삽입
		pq.add(new Node(v, 1));
		distance[v] = 0; //시작점이니까 distance는 0
		check[v] = true;
		
		//연결노드 distance 갱신
		for(int i = 1; i <= n; i++) {
			if(!check[i] && maps[v][i] != Integer.MAX_VALUE) {
				distance[i] = maps[v][i];
				pq.add(new Node(distance[i], i)); //우선순위 큐에 weight ← 정점의 가중치, i는 정점의 index
			}
		}
		
		while(!pq.isEmpty()) {
			int index;
			
			//노드 최소값 꺼내기 
			Node node = pq.poll(); //가장 최소값 
			index = node.index;
			
			check[index] = true;
			//distance 갱신
			for(int i = 1; i <= n; i++) {
				if(!check[i] && maps[index][i] != Integer.MAX_VALUE) {
					if(distance[i] > distance[index] + maps[index][i]) { //현재 노드를 거쳐가는 것이 더 짧으면
						distance[i] = distance[index] + maps[index][i];
						pq.add(new Node(distance[i], i));
					}
				}
			}			
		}
		
		for(int i = 1; i <= n; i++) {
			System.out.println(i + "번 노드까지 가는 최단 거리  : " + distance[i] + " ");
		}
		
	}
}

```
</details>

## 👀예제 코드 [BOJ 1753 : 최단경로]
인접리스트 + 우선순위 큐
<details markdown = "1">
<summary>코드</summary>

```Java
package boj_1753;

import java.util.*;
import java.io.*;
public class BOJ_1753 {	 
	static ArrayList<Node> [] list;
	static int distance[];	
	static final int INF = 100000000;
	static int V, E, K;
	
	static class Node implements Comparable<Node>{
		int weight;
		int index; 
		
		public Node(int index, int weight) {
			this.weight = weight;
			this.index = index;
		}
	
		@Override
		public int compareTo(Node node) {
			return Integer.compare(this.weight, node.weight);
		}		
	}
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
			
		String[] s1 = br.readLine().split(" ");
	    V = Integer.parseInt(s1[0]); //정점의 개수
	    E = Integer.parseInt(s1[1]); //간선의 개수
	    K = Integer.parseInt(br.readLine()); //시작점
	     
	    distance = new int[V + 1];		
		list = new ArrayList[V + 1];
		
		Arrays.fill(distance, INF);
		for (int i = 1; i <= V; i++) {
			list[i] = new ArrayList<>();
		}
   
	    for(int i = 0; i < E; i++) {
	    	String[] s2 = br.readLine().split(" ");
	        int start = Integer.parseInt(s2[0]);
	        int end = Integer.parseInt(s2[1]);
	        int weight = Integer.parseInt(s2[2]);	    
	        list[start].add(new Node(end, weight));
	    }
	     
	    dijkstra(K);
	    	   
		for(int i = 1; i < distance.length; i++) {
			if(distance[i] == INF)
				bw.write("INF");
			else
				bw.write(Integer.toString(distance[i]));
			bw.newLine();
		}
		
		bw.flush();
		bw.close();
	    
	    	     
	}
	public static void dijkstra(int v) {
		PriorityQueue<Node> pq = new PriorityQueue<>();
		boolean check[] = new boolean[V + 1];

		pq.add(new Node(v, 0));
		distance[v] = 0;
			
		while(!pq.isEmpty()) {		
			//노드 최소값 꺼내기 
			Node node = pq.poll(); //가장 최소값 
			int index = node.index;
			
			if(check[index])
				continue;
			check[index] = true;
			
			for(Node next : list[index]) {
				if(distance[next.index] > distance[index] + next.weight) {
					distance[next.index] = distance[index] + next.weight;
					pq.offer(new Node(next.index, distance[next.index]));
				}
			}
		}			
	}	
}
```
</details>

## 복잡도
- 배열 사용 : O(n²)
- 우선순위 큐 사용 : O((|V|+|E|)Log|V|)