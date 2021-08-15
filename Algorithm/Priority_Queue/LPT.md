# ⛓ 머신 스케줄링 
: 모든 기게를 풀 가동하여 가장 최소의 시간 안에 작업들을 모두 끝내는 것 

## 👉🏻LPT
## : longest processing time first
- 가장 긴 작업을 우선적으로 기계에 할당한다. </br>
    ![](/Images/lpt.JPG)

## 👉🏻알고리즘 
: 기계의 종료 시간이 중요!⭐</br>
- 종료 시간이 최소인 기계가 항상 선택되기 때문

-   ```
    1. 기계의 종료 시간 → *최소 히프*
    2. 최소 히프에서 기계를 꺼내 그 기계에 작업을 할당
    3. 기계의 종료 시간을 작업 시간만큼 증가시킨 후 다시 최소 히프에 넣기
    ```
## 💻LPT skeleton
```C
//LPT
#include <stdio.h>
#include <stdlib.h>
#define MAX_ELEMENT 20

typedef struct {
	int id;
	int available;
}element;
typedef struct {
	element heap[MAX_ELEMENT];
	int heap_size;
}HeapType;

HeapType* create() {
	return (HeapType*)malloc(sizeof(HeapType));
}

void init(HeapType* h) {
	h->heap_size = 0;
}
//기계의 종료시간을 최소 히프에 넣는다.
void insert(HeapType* h, element item) {
	int i;
	i = ++(h->heap_size);
	while (i != 1 && (item.available < h->heap[i / 2].available)) {
		h->heap[i] = h->heap[i / 2];
		i /= 2;
	}
	h->heap[i] = item; //자리에 item 넣기
}
//최소 히프에서 기계를 꺼낸다.
element delete_heap(HeapType* h) {
	int parent, child;
	element item, temp;

	item = h->heap[1];
	temp = h->heap[(h->heap_size)--]; //제일 말단 노드
	parent = 1;
	child = 2;
	while (child <= h->heap_size) {
		if (child < h->heap_size && (h->heap[child].available > h->heap[child + 1].available))
			child++;
		if (temp.available < h->heap[child].available) break; //말단 노드가 child보다 작으면 그 위에 있어야 함
		//level down
		h->heap[parent] = h->heap[child];
		parent = child;
		child *= 2;
	}
	h->heap[parent] = temp;
	return item; //어차피 반환하는 건 루트 노드 
}
#define JOBS 7
#define MACHINES 3
int main(void)
{
	int jobs[JOBS] = { 8, 7, 6, 5, 3, 2, 1 }; // 작업은 정렬되어 있다고 가정
	element m = { 0, 0 };
	HeapType* h;
	h = create();
	init(h);

	//여기서 available값은 기계가 사용하게 되는 시간
	for (int i = 0; i < MACHINES; i++) {
		m.id = i + 1;
		m.available = 0;
		insert(h, m);
	}

	// 최소 히프에서 기계를 꺼내서 작업을 할당하고 사용가능 시간을 증가시킨 후에
	// 다시 최소 히프에 추가한다.
		for (int i = 0; i < JOBS; i++) {
			m = delete_heap(h);
			printf("JOB %d을 시간=%d부터 시간=%d까지 기계 %d번에 할당한다. \n",i, m.available, m.available + jobs[i] - 1, m.id);
			m.available += jobs[i];
			insert_max_heap(h, m);
		}
	return 0;
}
```
