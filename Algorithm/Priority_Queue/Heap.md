# 🌄Heap
[히프](#히프) </br>
[히프 정렬](/Algorithm/Priority_Queue/Heap_Sorting.md) </br>
[머신 스케줄링](/Algorithm/Priority_Queue/LPT.md)
## 히프
: 완전 이진 트리의 일종으로 우선순위 큐를 위하여 특별히 만들어진 자료구조
- Key(부모노드) >= key(자식노드)
- ![](/Images/heap개념.JPG)

### 👉🏻목적
: 삭제 연산이 수행될 때마다 가장 큰 값을 찾아내기 위함 == **루트노드** </br>
=> *전체 정렬 필요성 X*

### 👉🏻종류
- `최대히프 (max heap)` : key(부모노드) >= key(자식노드)
- `최소 히프(min heap)` : key(부모노드) <= key(자식노드)

### 👉🏻히프의 높이
: n개의 노드를 가지고 있는 히프의 높이는 O(logn)</br>
- 히프는 완전 이진 트리
- 마지막 level h를 제외하고는 각 level i에 2^(i-1)개의 노드가 존재

---
</br>

### 👉🏻구현
: 배열을 이용하여 구현
- 완전 이진트리이므로 각 노드에 번호를 붙일 수 있다.
    - 이 번호를 배열의 인덱스라고 생각! </br>
        ```
        1. 왼쪽 자식의 인덱스 = (부모의 인덱스) * 2
        2. 오른쪽 자식의 인덱스 = (부모의 인덱스) * 2 + 1
        3. 부모의 인덱스 = (자식의 인덱스) / 2
        ```
        ![](/Images/heap구현.JPG)

### 👉🏻히프의 정의 
```C
typedef struct{
    int key;
}element;
typedef struct{
    element heap[MAX_ELEMENT];
    int heap_size;
}HeapType;

HeapType heap; //정적 메모리 할당 사용
HeapType *heap = create(); //동적 메모리 할당 사용
```

### 👉🏻히프 삽입
: 신입사원을 일단 말단자리에 앉히고, 능력에 따라 승진시키는 것과 비슷하다. </br>
1. 히프에 새로운 요소가 들어오면, 일단 새로운 노드를 히프의 마지막 노드에 이어서 삽입한다.
2 삽입 후에 새로운 노드를 부모 노드들과 교환해서 히프의 성질을 만족시킨다.

### 👉🏻upheap 연산
 ![](/Images/upheap.JPG)

- **알고리즘**
    ```
    1. 히프 크기를 하나 증가시킨다.
    2. 증가된 히프 크기 위치에 새로운 노드를 삽입한다.
    3. i가 루트 노드가 아니고, i번째 노드가 i의 부모노드보다 크면 i번째 노드와 부모 노드를 교환
    4. i번째 노드와 부모 노드를 교환
    5. 한 레벨 위로 올라간다. (승진)
    ```
    ```C
    void insert_min_heap(HeapType* h, element item) {
        int i;
        i = ++(h->heap_size);
        while (i != 1 && (item.key > h->heap[i / 2].key)) {
            h->heap[i] = h->heap[i / 2];
            i /= 2;
        }
        h->heap[i] = item; //자리에 item 넣기
    }
    ```

### 👉🏻히프 삭제
: 사장의 자리가 비게되면 먼저 제일 말단 사원을 사장 자리로 앉힌 다음, 능력에 따라 강등시킨다.
1. 루트 노드를 삭제한다.
2. 마지막 노드를 루트 노드로 이동한다.
3. 루트에서부터 단말 노드까지의 경로에 있는 노드들을 교환하여 히프 성질을 만족시킨다.

### 👉🏻downheap 연산
 ![](/Images/downheap.JPG)

 - **알고리즘**
    ```
    1. 루트 노드 값을 반환을 위하여 item 변수로 옮긴다.
    2. 말단 노드를 루트 노드로 옮긴다.
    3. 히프의 크기를 하나 줄인다.
    4. 루트의 왼쪽 자식부터 비교를 시작한다.
    5. i가 히프 트리의 크기보다 작으면(즉, 히프트리를 벗어나지 않으면)
    6. 오른쪽 자식이 더 크면
    7-8. 두개의 자식노드 中 큰 값의 인덱스를 largest로 옮긴다.
    9. largest의 부모노드가 largest보다 크면
    10. 중지
    11. 그렇지 않으면, largest와 largest 부모노드를 교환한다.
    12. 한 레벨 밑으로 내려간다.
    13. 최대 값을 반환한다.
    ```
    ```C
    element delete_max_heap(HeapType* h) {
        int parent, child;
        element item, temp;

        item = h->heap[1];
        temp = h->heap[(h->heap_size)--]; //제일 말단 노드
        parent = 1;
        child = 2;
        while (child <= h->heap_size) {
            if(child < h->heap_size && (h->heap[child].key < h->heap[child + 1].key))
                child++;
            if (temp.key >= h->heap[child].key) break; //말단 노드가 child보다 크면 그 위에 있어야 함
            //level down
            h->heap[parent] = h->heap[child];
            parent = child;
            child *= 2;
        }
        h->heap[parent] = temp;
        return item; //어차피 반환하는 건 루트 노드 
    }
    ```

### 💻heap skeleton
<details markdown="1">
<summary>max_heap 코드 보기👀</summary>

```C
//heap insert/delete
#include <stdio.h>
#include <stdlib.h>
#define MAX_ELEMENT 20

typedef struct {
	int key;
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

void insert_max_heap(HeapType* h, element item) {
	int i;
	i = ++(h->heap_size);
	while (i != 1 && (item.key > h->heap[i / 2].key)) {
		h->heap[i] = h->heap[i / 2];
		i /= 2;
	}
	h->heap[i] = item; //자리에 item 넣기
}

element delete_max_heap(HeapType* h) {
	int parent, child;
	element item, temp;

	item = h->heap[1];
	temp = h->heap[(h->heap_size)--]; //제일 말단 노드
	parent = 1;
	child = 2;
	while (child <= h->heap_size) {
		if(child < h->heap_size && (h->heap[child].key < h->heap[child + 1].key))
			child++;
		if (temp.key >= h->heap[child].key) break; //말단 노드가 child보다 크면 그 위에 있어야 함
		//level down
		h->heap[parent] = h->heap[child];
		parent = child;
		child *= 2;
	}
	h->heap[parent] = temp;
	return item; //어차피 반환하는 건 루트 노드 
}
int main(void)
{
	element e1 = { 10 }, e2 = { 5 }, e3 = { 30 };
	element e4, e5, e6;
	HeapType* heap;
	heap = create(); // 히프 생성
	init(heap); // 초기화
	// 삽입
	insert_max_heap(heap, e1);
	insert_max_heap(heap, e2);
	insert_max_heap(heap, e3);
	// 삭제
	e4 = delete_max_heap(heap);
	printf("< %d > ", e4.key);
	e5 = delete_max_heap(heap);
	printf("< %d > ", e5.key);
	e6 = delete_max_heap(heap);
	printf("< %d > \n", e6.key);
	free(heap);
	return 0;
}
```

</details>

---
</br>

### 👉🏻복잡도 분석 
- `삽입` : 최악의 경우, 루트 노드까지 올라가야 하므로 트리의 높이에 해당하는 비교연산 및 이동연산 필요!
    - **O(logn)**

- `삭제` : 최악의 경우, 가장 아래 레벨까지 내려가야하므로 역시 트리의 높이만큼의 시간이 걸린다.
    - **O(logn)**

---
</br>



