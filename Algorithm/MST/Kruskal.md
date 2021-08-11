# 🥞Kruskal MST

## 🎲알고리즘
: **탐욕적인 방법 [greedy method]** </br> 

- 각 단계에서 최선의 답을 선택하는 과정을 반복함으로써 최종적인 해답에 도달
- 항상 최적의 해답을 주는 지 검증필요
     - _Kruskal_ 은 증명됨!

- 그래프의 간선들을 오름차순으로 정렬
-  정렬된 간선들의 리스트에서 **사이클을 형성하지 않는 간선**을 찾아 현재의 MST 집합에 추가한다.
- 만약 사이클을 형성하면 그 간선은 제외된다.

**🌟`사이클이 생기지 않게 하려면 어떻게 해야할까?`**
- 서로 다른 집합에 속하는 정점을 연결해야한다.
 </br>== 추가하고자 하는 간선의 양 끝 정점이 같은 집합에 속해있는지 검사한다.
    - 검사 : **`union-find`**

### `union-find` 
- union(x,y) : x, y가 속해있는 집합을 입력으로 받아 2개의 집합의 합집합을 만든다.
- find (x) : 원소 x가 속해있는 집합을 반환한다.
    - ex) {1}, {2}, {3}, {4}, {5}, {6} </br>
            -> union(1,4), union(5,2)
            => {1, 4}, {5, 2}, {3}, {6}
---
</br>

## ⛳구현 
- 비트벡터, 배열, 연결리스트 ...
- 가장 효율적인 방법 :  **트리**
    - `부모 포인터 표현` :  각노드에 대해 그 노드의 부모에 대한 포인터만 저장 
        - 노드의 가장 왼쪽/오른쪽 자식을 찾는 작업에는 ❌
        - but, 두 노드가 같은 트리에 있는가?  ⭕

        - 배열로 구현 가능  
            - 부모노드의 인덱스 저장, 배열의 값이 -1 이면 부모 노드가 없는 것!

                |A|B|C|D|E|
                |:-:|:-:|:-:|:-:|:-:|
                -1|-1|-1|-1|-1

                *union(A, B)* 

                |A|B|C|D|E|                     
                |:-:|:-:|:-:|:-:|:-:|
                -1|0|-1|-1|-1
                
                : B의 0은 A의 idx

                *union(C, E)*

                |A|B|C|D|E|
                |:-:|:-:|:-:|:-:|:-:|
                -1|0|-1|-1|2

                : E의 2는 C의 idx

- `void set_init(n)` : 6을 넣으면 {0} ... {5}
- `int set_find(정점)` : 정점이 속하는 집합 반환
- `void set_union(대표정점1, 대표정점2)` : 두 개의 원소가 속한 집합을 합친다. 
----
</br>


## 👀그림으로 확인 

 ![kruskal](/Images/kruskal.JPG)

 1. 간선 정렬 : qsort() 사용
    - [qsort 개념](/C_Standard_Library/qsort.md)

2. `set_find`를 사용해 같은 집합에 있는지 확인한다.
3. 서로 다른 집합이라면 == 사이클이 형성되지 않는다면 </br>`set_union`을 사용해 두 개의 집합을 합친다.
4. 같은 집합이라면 선택하지 않는다.

---
</br>

## ⚙시간 복잡도
`union-find` 알고리즘을 활용하면 **간선들을 정렬하는 시간**에 좌우된다. </br>
효율적인 정렬 알고리즘을 사용한다면 : *|e|log2^|e|*
- qsort의 평균적인 경우 : O(log2^n)으로 정렬 알고리즘 中 가장 빠르다.

</br>

---
</br>

## 📎예제 문제로 확인하기 
*1197-최소 스패닝 트리*
- 기존 kruskal 코드에 가중치의 합만 추가로 구현하여 출력하면 되는 문제!

```C
//1197 - 최소 스패닝 트리
#include <stdio.h>
#include <stdlib.h>

#define MAX_VERTICES 10010
#define MAX_EDGE 100001
#define INF 2147483648

int parent[MAX_VERTICES];
int v, e;
int edgeCnt;

void set_init(int n) {
	for (int i = 1; i <= n; i++) {
		parent[i] = -1;
	}
}

int set_find(int curr) {
	if (parent[curr] == -1)
		return curr; //curr이 부모노드일때(root)
	while (parent[curr] != -1)
		curr = parent[curr];
	return curr;
}

void set_union(int a, int b) {
	int root1 = set_find(a);
	int root2 = set_find(b);
	if (root1 != root2)
		parent[root1] = root2;
}

struct Edge { //간선을 나타내는 구조체
	int start, end, weight;
};
typedef struct GraphType {
	int n;
	struct Edge edges[MAX_EDGE];
}GraphType;

//그래프 초기화
void graph_init(GraphType* g) {
	g->n = 0;
	for (int i = 0; i < MAX_EDGE; i++) {
		g->edges[i].start = 0;
		g->edges[i].end = 0;
		g->edges[i].weight = INF;
	}
}
//간선 삽입 연산 
void insert_edge(GraphType* g, int start, int end, int w, int cnt) {
	g->edges[cnt].start = start;
	g->edges[cnt].end = end;
	g->edges[cnt].weight = w;
}

//compare
int compare(const void* a, const void* b) {
	struct Edge* x = (struct Edge*)a;
	struct Edge* y = (struct Edge*)b;
	return (x->weight - y->weight);
}

//kruskal
int kruskal(GraphType* g) {
	int edge_accepted = 0; //현재까지 선택된 간선의 수
	int uset, vset, temp = 0;
	struct Edge edge;

	set_init(g->n);
	qsort(g->edges, edgeCnt, sizeof(struct Edge), compare);

	int i = 0;
	while (edge_accepted < (g->n - 1)) {
		edge = g->edges[i];
		uset = set_find(edge.start);
		vset = set_find(edge.end);

		if (uset != vset) {
			temp += edge.weight;
			edge_accepted++;
			set_union(uset, vset);
		}
		i++;
	}	
	return temp;
}

int main(void) {
	GraphType g;
	int start, end, weight;

	scanf_s("%d %d", &v, &e);
	g.n = v;

	edgeCnt = 0;
	for (int i = 0; i < e; i++) {
		scanf_s("%d %d %d", &start, &end, &weight);
		insert_edge(&g, start, end, weight, edgeCnt++);
	}

	printf("%d", kruskal(&g));

	return 0;
}
```
