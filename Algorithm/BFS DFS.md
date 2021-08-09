# BFS/DFS

## ⭐`DFS`
`깊이 우선 탐색 `
- **정의** : 한 경로의 끝까지 최대한 깊숙히 탐색하다가 그 다음 경로로 이동한다. 
	
- **장점** : 현재 경로의 노드만 기억하면 됨 -> 저장공간이 많이 필요하지않다.
- **단점** : 
	- 목표 노드까지 도달한 경로가 최단 경로라는 보장이 없다.
	- 해가 없는 경로인 경우 </br>:  끝까지 탐색하기 때문에 미리 정해둔 임의의 깊이까지만 탐색하고 해를 발견하지 못하면 가장 최근의 부모 노드로 돌아가는  _백트래킹(Back Tracking)_ 을 이용해 다른 경로를 선택하여 진행한다.
- **구현** : 재귀 / 스택(stack)
	- 의사 코드
	```C
	Dfs(G, v):
		스택 s를 생성한다.
		s.push(v)
		while (not is_empty(s)) do
			v = s.pop()
			if(v가 방문되지 않았으면)
				v를 방문되었다고 표시
				for all u ∈ (v에 인접한 정점) do
					if(u가 아직 방문되지 않았으면)
						s.push(u)
	```

	- 그림 설명

	![DFS](./Images/DFS(stack).jpg)

## 🌙`BFS`
`넓이 우선 탐색`
- **정의** : 시작정점에서 가까운 노드부터 탐색
- **장점** : 최단 경로를 보장한다.
- **단점** : 
	- 경로가 매우 길다면, 경로까지 탐색하는 중간 노드의 수가 급격히 증가하므로 저장공간이 많이 필요하다.
	- 해가 깊은 곳에 있는 경우 DFS보다 느리다.
	- 해가 없는 경로인 경우 </br>: 모든 경로를 탐색한 다음 끝난다.
- **구현** : 큐(queue)
	- 재귀적으로 동작하지 않는다.

	- 의사 코드
	```C
	Bfs(v):
		v를 방문되었다고 표시;
		큐 q에 정점 v를 삽입;
		while(q가 공백이 아니면) do
			q에서 정점 w를 삭제;
			for all u ∈ (w에 인접한 정점) do
				if(u가 아직 방문되지 않았으면)
					then u를 큐에 삽입;
						u를 방문되었다고 표시;
	```

	- 그림 설명

	![BFS](./Images/BFS(queue).jpg)

___
## 👉`GRAPH`
## 시간복잡도
>인접행렬 </br>

`DFS`
- 두 정점을 연결하는 간선의 존재 여부 : O(1)
     - M[u][v] 값 조사
- 정점의 차수 : O(n)
- 그래프에 존재하는 모든 간선의 수 : O(n^2)
    - 인접행렬 전체를 조사해야하므로 n^2번의 조사가 필요하다.

`BFS`
- O(n^2)
</br></br>


>인접리스트 </br>

`DFS`
- O(n + e)
    - 간선 (i, j)의 존재 여부나 정점 i의 차수를 알기 위해서는 인접리스트에서의 정점 i의 연결리스트를 탐색해야함
        </br>
        ->연결 리스트에 있는 노드의 수 만큼, 즉 정점차수만큼의 시간이 필요
        </br></br>
        - => n개의 정점과 e개의 간선을 가진 그래프에서 전체 간선의 수를 알아내려면 헤더노드를 포함하여 모든 인접리스트를 조사해야함

`BFS`
- O(n + e)

___
</br>


## 코드로 구현
### `인접행렬로 구현한 DFS`
```C
void dfs_mat(GraphType *g, int v) 
{
     int w;
     visited[v] = 1;
     printf("%d ", v);

     for (w = 0; w < g->n; w++)
          if ((g->adj_mat[v][w] == 1) && (visited[w] == 0)) { // w가 인접한 정점이고 w가 아직 방문되지 않았으면
              dfs_mat(g, w);	   
          }
}
```

### `인접리스트로 구현한 DFS`
```C
void dfs(GraphType* g, int v) {
	GraphNode* w;
	visited[v] = TRUE;
	printf("%d ", v);

	for (w = g->adj_list[v]; w != NULL; w = w->link) {
		if (!visited[w->vertex])		
			dfs(g, w->vertex);
	}
}
```

### `인접리스트로 구현한 BFS`
```C
void bfs(GraphType* g, int v) {
	GraphNode* w;
	QueueType q;
	init_queue(&q);

	visited[v] = TRUE;
	printf("%d ", v);

	enqueue(&q, v);

	while (!is_empty(&q)) {
		v = dequeue(&q); //큐에서 시작정점을 꺼낸 후 
		for (w = g->adj_list[v]; w != NULL; w = w->link) {
			if (!visited[w->vertex]) {
				visited[w->vertex] = TRUE;
				printf("%d ", w->vertex); 
				enqueue(&q, w->vertex); // 시작정점의 인접 정점들을 큐에 추가한다.
			}
		}
	}
}
```
