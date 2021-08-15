# 🍮Prim
: 시작정점에서부터 출발하여 신장트리 집합을 단게적으로 확장해나가는 방법 </br>
: 신장 트리 집합에 인접한 정점 中 최저 간선으로 연결된 정점 선택하여 **신장트리 집합에 추가한다.**(→ 집합에 정점의 개수가 n-1개가 될 때까지) </br>

![](/Images/prim.JPG)

---
</br>

## 👉🏻Kruskal & Prim 의 차이 
|kruskal|Prim|
|:-:|:-:|
시작정점X</br>간선 선택 기반 | 시작정점 O </br>정점 선택 기반
최소 간선 선택 </br>(n-1) | <신장 트리 집합>에서 가장 가까운 정점 선택 </br> (모든 정점이 선택됨)

## 👀알고리즘 
- ### `distance[]` : 정점의 개수 크기의 배열 
    - 현재까지 알려진, 신장트리 정점 집합에서 각 정점까지의 거리를 가지고 있음
    - 처음에는 시작노드만 0, 나머지는 ∞
        - 트리 집합에 아무것도 없기 때문!

- ### `selected[]` : 신장 트리 집합에 선택 되었는 지?

 1. 우선순위 큐(min heap)(or 배열)에 모든 정점을 삽입한다.
    - 우선순위 : distance 배열
2. 가장 작은 distance를 가지는 정점을 꺼낸다.
    - 이 정점이 트리 집합에 추가된다.
3. 트리 집합에 새로운 정점 u가 추가된다.
    - u에 인접한 정점 v들의 distance 값을 변경한다.
        ```
        if(기존 dist[v]보다 간선(u, v)값이 작으면)
            distance[v] = 간선(u, v)값 (== 가중치)
        ```
4. Q에 있는 모든 정점들이 소진될 때까지 반복

- 한번 선택된 정점은 다시 선택 ❌
- 트리 집합에 인접하지 않은 정점들의 distance 값은 ∞ → 선택 ❌
- 우선 순위 큐로 구현 시 우선 순위를 중간중간 변경시켜야 함!

- ### `int get_min_vertex(int n)` : 최소 distance[v]값을 갖는 정점 반환
    - 
        ```C
        //최소 distance [v] 값을 갖는 정점을 반환
        int get_min_vertex(int n) {
            int v = 0;

            for (int i = 1; i <= n; i++)
                if (!selected[i]) {
                    v = i;
                    break;
                }
            for (int i = 1; i <= n;i++) {
                if (!selected[i] && (distance[i] < distance[v]))
                    v = i;
            }
            return v;
        }
        ```

---
</br>

## 💻구현
![](/Images/prim구현.JPG)

- `0 선택` : 인접 v == 1, 3, 4 → distance 재조정 | selected[0] = TRUE
- `1 선택` : 인접 v == 0, 3, 2, 4 → distance 재조정 | selected[1] = TRUE | v == 3은 원래 distance가 더 작기 때문에 변경 ❌
- `3 선택` : 인접 v == 0, 1, 5 → distance 재조정 | selected[3] = TRUE | v == 1은 원래 distance가 더 작기 때문에 변경 ❌
- `2 선택` : 인접 v == 1, 4, 5 → distance 재조정 | selected[2] = TRUE | v == 5는 원래 distance가 더 작기 때문에 변경 ❌
- `4 선택` : 인접 v == 0, 1, 2 → distance 재조정 | selected[4] = TRUE
- `5 선택` : 인접 v == 2, 3 → distance 재조정 | selected[5] = TRUE

</br>


## 💻prim skeleton
<details markdown="1">
<summary>prim 코드 보기👀</summary>

```C
//Prim skeleton (우선순위큐-배열로 구현)
#include <stdio.h>
#include <stdlib.h>

#define INF 1000L
#define MAX_VERTICES 100

typedef struct GraphType {
	int n;
	int weight[MAX_VERTICES][INF];
}GraphType;

int selected[MAX_VERTICES];
int distance[MAX_VERTICES];


//최소 distance [v] 값을 갖는 정점을 반환
int get_min_vertex(int n) {
	int v = 0;

	GraphType g;
	for (int i = 0; i < n; i++) 
		if (!selected[i]) {
			v = i;
			break;
		}
	for (int i = 0; i < n;i++) {
		if (!selected[i] && (distance[i] < distance[v]))
			v = i;
	}
	return v;
}

void prim(GraphType* g, int s) { //s == start
	int u, v;

	for (u = 0; u < g->n; u++)
		distance[u] = INF; // 모든 정점 삽입과 동시에 거리 초기화
	distance[s] = 0;

	for (int i = 0; i < g->n; i++) {
		u = get_min_vertex(g->n); //가장 작은 distance를 가지는 정점을 꺼낸다.
		selected[u] = 1; //트리 집합에 새로운 정점 u가 추가됨
		if (distance[u] == INF)return; //비연결그래프일때
		printf("정점 %d 추가\n", u);

		for (v = 0; v < g->n; v++) {
			if (g->weight[u][v] != INF) { //인접한 정점찾기 (0,1) 이 무한대면 인접정점이아님!
				if (!selected[v] && (g->weight[u][v] < distance[v]))
					distance[v] = g->weight[u][v];
			}
		}
	}
}
int main(void)
{
	GraphType g = { 7,
	{{ 0, 29, INF, INF, INF, 10, INF },
	{ 29, 0, 16, INF, INF, INF, 15 },
	{ INF, 16, 0, 12, INF, INF, INF },
	{ INF, INF, 12, 0, 22, INF, 18 },
	{ INF, INF, INF, 22, 0, 27, 25 },
	{ 10, INF, INF, INF, 27, 0, INF },
	{ INF, 15, INF, 18, 25, INF, 0 } }
	};
	prim(&g, 0);
	return 0;
}
```
</details>

---
</br>


## 👉🏻복잡도 
: 주 반복문이 정점의 수 n만큼 반복, 내부 반복문이 n번 반복
### → O(n²)
∴ </br>
`희소 그래프` → kruskal이 적합 </br>
`밀집 그래프` → prim이 유리

        