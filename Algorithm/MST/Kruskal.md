# π₯Kruskal MST

## π²μκ³ λ¦¬μ¦
: **νμμ μΈ λ°©λ² [greedy method]** </br> 

- κ° λ¨κ³μμ μ΅μ μ λ΅μ μ ννλ κ³Όμ μ λ°λ³΅ν¨μΌλ‘μ¨ μ΅μ’μ μΈ ν΄λ΅μ λλ¬
- ν­μ μ΅μ μ ν΄λ΅μ μ£Όλ μ§ κ²μ¦νμ
     - _Kruskal_ μ μ¦λͺλ¨!

- κ·Έλνμ κ°μ λ€μ μ€λ¦μ°¨μμΌλ‘ μ λ ¬
-  μ λ ¬λ κ°μ λ€μ λ¦¬μ€νΈμμ **μ¬μ΄ν΄μ νμ±νμ§ μλ κ°μ **μ μ°Ύμ νμ¬μ MST μ§ν©μ μΆκ°νλ€.
- λ§μ½ μ¬μ΄ν΄μ νμ±νλ©΄ κ·Έ κ°μ μ μ μΈλλ€.

**π`μ¬μ΄ν΄μ΄ μκΈ°μ§ μκ² νλ €λ©΄ μ΄λ»κ² ν΄μΌν κΉ?`**
- μλ‘ λ€λ₯Έ μ§ν©μ μνλ μ μ μ μ°κ²°ν΄μΌνλ€.
 </br>== μΆκ°νκ³ μ νλ κ°μ μ μ λ μ μ μ΄ κ°μ μ§ν©μ μν΄μλμ§ κ²μ¬νλ€.
    - κ²μ¬ : **`union-find`**

### `union-find` 
- union(x,y) : x, yκ° μν΄μλ μ§ν©μ μλ ₯μΌλ‘ λ°μ 2κ°μ μ§ν©μ ν©μ§ν©μ λ§λ λ€.
- find (x) : μμ xκ° μν΄μλ μ§ν©μ λ°ννλ€.
    - ex) {1}, {2}, {3}, {4}, {5}, {6} </br>
            -> union(1,4), union(5,2)
            => {1, 4}, {5, 2}, {3}, {6}
---
</br>

## β³κ΅¬ν 
- λΉνΈλ²‘ν°, λ°°μ΄, μ°κ²°λ¦¬μ€νΈ ...
- κ°μ₯ ν¨μ¨μ μΈ λ°©λ² :  **νΈλ¦¬**
    - `λΆλͺ¨ ν¬μΈν° νν` :  κ°λΈλμ λν΄ κ·Έ λΈλμ λΆλͺ¨μ λν ν¬μΈν°λ§ μ μ₯ 
        - λΈλμ κ°μ₯ μΌμͺ½/μ€λ₯Έμͺ½ μμμ μ°Ύλ μμμλ β
        - but, λ λΈλκ° κ°μ νΈλ¦¬μ μλκ°?  β­

        - λ°°μ΄λ‘ κ΅¬ν κ°λ₯  
            - λΆλͺ¨λΈλμ μΈλ±μ€ μ μ₯, λ°°μ΄μ κ°μ΄ -1 μ΄λ©΄ λΆλͺ¨ λΈλκ° μλ κ²!

                |A|B|C|D|E|
                |:-:|:-:|:-:|:-:|:-:|
                -1|-1|-1|-1|-1

                *union(A, B)* 

                |A|B|C|D|E|                     
                |:-:|:-:|:-:|:-:|:-:|
                -1|0|-1|-1|-1
                
                : Bμ 0μ Aμ idx

                *union(C, E)*

                |A|B|C|D|E|
                |:-:|:-:|:-:|:-:|:-:|
                -1|0|-1|-1|2

                : Eμ 2λ Cμ idx

- `void set_init(n)` : 6μ λ£μΌλ©΄ {0} ... {5}
- `int set_find(μ μ )` : μ μ μ΄ μνλ μ§ν© λ°ν
- `void set_union(λνμ μ 1, λνμ μ 2)` : λ κ°μ μμκ° μν μ§ν©μ ν©μΉλ€. 
----
</br>


## πκ·Έλ¦ΌμΌλ‘ νμΈ 

 ![kruskal](/Images/kruskal.JPG)

 1. κ°μ  μ λ ¬ : qsort() μ¬μ©
    - [qsort κ°λ](/C_Standard_Library/qsort.md)

2. `set_find`λ₯Ό μ¬μ©ν΄ κ°μ μ§ν©μ μλμ§ νμΈνλ€.
3. μλ‘ λ€λ₯Έ μ§ν©μ΄λΌλ©΄ == μ¬μ΄ν΄μ΄ νμ±λμ§ μλλ€λ©΄ </br>`set_union`μ μ¬μ©ν΄ λ κ°μ μ§ν©μ ν©μΉλ€.
4. κ°μ μ§ν©μ΄λΌλ©΄ μ ννμ§ μλλ€.

---
</br>

## βμκ° λ³΅μ‘λ
`union-find` μκ³ λ¦¬μ¦μ νμ©νλ©΄ **κ°μ λ€μ μ λ ¬νλ μκ°**μ μ’μ°λλ€. </br>
ν¨μ¨μ μΈ μ λ ¬ μκ³ λ¦¬μ¦μ μ¬μ©νλ€λ©΄ : *|e|log2^|e|*
- qsortμ νκ· μ μΈ κ²½μ° : O(log2^n)μΌλ‘ μ λ ¬ μκ³ λ¦¬μ¦ δΈ­ κ°μ₯ λΉ λ₯΄λ€.

</br>

---
</br>

## πμμ  λ¬Έμ λ‘ νμΈνκΈ° 
*1197-μ΅μ μ€ν¨λ νΈλ¦¬*
- κΈ°μ‘΄ kruskal μ½λμ κ°μ€μΉμ ν©λ§ μΆκ°λ‘ κ΅¬ννμ¬ μΆλ ₯νλ©΄ λλ λ¬Έμ !

```C
//1197 - μ΅μ μ€ν¨λ νΈλ¦¬
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
		return curr; //currμ΄ λΆλͺ¨λΈλμΌλ(root)
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

struct Edge { //κ°μ μ λνλ΄λ κ΅¬μ‘°μ²΄
	int start, end, weight;
};
typedef struct GraphType {
	int n;
	struct Edge edges[MAX_EDGE];
}GraphType;

//κ·Έλν μ΄κΈ°ν
void graph_init(GraphType* g) {
	g->n = 0;
	for (int i = 0; i < MAX_EDGE; i++) {
		g->edges[i].start = 0;
		g->edges[i].end = 0;
		g->edges[i].weight = INF;
	}
}
//κ°μ  μ½μ μ°μ° 
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
	int edge_accepted = 0; //νμ¬κΉμ§ μ νλ κ°μ μ μ
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
