# πνν μ λ ¬

: ννλ₯Ό μ΄μ©νλ©΄ μ λ ¬ κ°λ₯ 
1. λ¨Όμ  μ λ ¬ν΄μΌ ν  nκ°μ μμλ€μ μ΅λ heapμ μ½μ
2. νλ²μ νλμ© μμλ₯Ό ννμμ μ­μ νμ¬ μ μ₯νλ©΄ λ¨
- μ΅μνν : μ€λ¦μ°¨μ / μ΅λνν : λ΄λ¦Όμ°¨μ
- νλμ μμλ₯Ό ννμ μ½μ / μ­μ  -> O(log n)
    - μμμ κ°μλ nκ° μ΄λ―λ‘ => **O(nlogn)**
- μ΅λλ‘ μ μ©ν κ²½μ° : μ μ²΄ μλ£λ₯Ό μ λ ¬νλ κ²μ΄ μλλΌ κ°μ₯ ν° κ° λͺκ°λ§ νμν  λ 
    => **ννμ λ ¬**

## π»heap sorting skeleton

```C
//heap sorting
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

void insert(HeapType* h, element item) {
	int i;
	i = ++(h->heap_size);
	while (i != 1 && (item.key > h->heap[i / 2].key)) {
		h->heap[i] = h->heap[i / 2];
		i /= 2;
	}
	h->heap[i] = item; //μλ¦¬μ item λ£κΈ°
}

element delete_heap(HeapType* h) {
	int parent, child;
	element item, temp;

	item = h->heap[1];
	temp = h->heap[(h->heap_size)--]; //μ μΌ λ§λ¨ λΈλ
	parent = 1;
	child = 2;
	while (child <= h->heap_size) {
		if (child < h->heap_size && (h->heap[child].key < h->heap[child + 1].key))
			child++;
		if (temp.key >= h->heap[child].key) break; //λ§λ¨ λΈλκ° childλ³΄λ€ ν¬λ©΄ κ·Έ μμ μμ΄μΌ ν¨
		//level down
		h->heap[parent] = h->heap[child];
		parent = child;
		child *= 2;
	}
	h->heap[parent] = temp;
	return item; //μ΄μ°¨νΌ λ°ννλ κ±΄ λ£¨νΈ λΈλ 
}

void heap_sorting(element arr[], int n) {
	HeapType* h;
	h = create();
	init(h);
	for (int i = 0; i < n; i++) {
		insert(h, arr[i]);
	}
	printf("μ€λ¦μ°¨μ:");
	for (int i = n - 1; i >= 0; i--) {
		arr[i] = delete_heap(h);
	}

	/*printf("\nλ΄λ¦Όμ°¨μ:");
	for (int i = 0; i < n; i++) {
		arr[i] = delete_heap(h);
	}*/
	free(h);
}
#define SIZE 8
int main(void)
{
	element list[SIZE] = { 23, 56, 11, 9, 56, 99, 27, 34 };
	heap_sorting(list, SIZE);
	for (int i = 0; i < SIZE; i++) {
		printf("%d ", list[i].key);
	}
	printf("\n");
	return 0;
}
```