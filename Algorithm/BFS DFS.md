# BFS/DFS

## `DFS`
- 깊이 우선 탐색 
## `BFS`
- 넓이 우선 탐색

___
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
