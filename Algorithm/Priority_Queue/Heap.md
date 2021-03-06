# πHeap
[νν](#νν) </br>
[νν μ λ ¬](/Algorithm/Priority_Queue/Heap_Sorting.md) </br>
[λ¨Έμ  μ€μΌμ€λ§](/Algorithm/Priority_Queue/LPT.md)
## νν
: μμ  μ΄μ§ νΈλ¦¬μ μΌμ’μΌλ‘ μ°μ μμ νλ₯Ό μνμ¬ νΉλ³ν λ§λ€μ΄μ§ μλ£κ΅¬μ‘°
- Key(λΆλͺ¨λΈλ) >= key(μμλΈλ)
- ![](/Images/heapκ°λ.JPG)

### ππ»λͺ©μ 
: μ­μ  μ°μ°μ΄ μνλ  λλ§λ€ κ°μ₯ ν° κ°μ μ°Ύμλ΄κΈ° μν¨ == **λ£¨νΈλΈλ** </br>
=> *μ μ²΄ μ λ ¬ νμμ± X*

### ππ»μ’λ₯
- `μ΅λνν (max heap)` : key(λΆλͺ¨λΈλ) >= key(μμλΈλ)
- `μ΅μ νν(min heap)` : key(λΆλͺ¨λΈλ) <= key(μμλΈλ)

### ππ»ννμ λμ΄
: nκ°μ λΈλλ₯Ό κ°μ§κ³  μλ ννμ λμ΄λ O(logn)</br>
- ννλ μμ  μ΄μ§ νΈλ¦¬
- λ§μ§λ§ level hλ₯Ό μ μΈνκ³ λ κ° level iμ 2^(i-1)κ°μ λΈλκ° μ‘΄μ¬

---
</br>

### ππ»κ΅¬ν
: λ°°μ΄μ μ΄μ©νμ¬ κ΅¬ν
- μμ  μ΄μ§νΈλ¦¬μ΄λ―λ‘ κ° λΈλμ λ²νΈλ₯Ό λΆμΌ μ μλ€.
    - μ΄ λ²νΈλ₯Ό λ°°μ΄μ μΈλ±μ€λΌκ³  μκ°! </br>
        ```
        1. μΌμͺ½ μμμ μΈλ±μ€ = (λΆλͺ¨μ μΈλ±μ€) * 2
        2. μ€λ₯Έμͺ½ μμμ μΈλ±μ€ = (λΆλͺ¨μ μΈλ±μ€) * 2 + 1
        3. λΆλͺ¨μ μΈλ±μ€ = (μμμ μΈλ±μ€) / 2
        ```
        ![](/Images/heapκ΅¬ν.JPG)

### ππ»ννμ μ μ 
```C
typedef struct{
    int key;
}element;
typedef struct{
    element heap[MAX_ELEMENT];
    int heap_size;
}HeapType;

HeapType heap; //μ μ  λ©λͺ¨λ¦¬ ν λΉ μ¬μ©
HeapType *heap = create(); //λμ  λ©λͺ¨λ¦¬ ν λΉ μ¬μ©
```

### ππ»νν μ½μ
: μ μμ¬μμ μΌλ¨ λ§λ¨μλ¦¬μ μνκ³ , λ₯λ ₯μ λ°λΌ μΉμ§μν€λ κ²κ³Ό λΉμ·νλ€. </br>
1. ννμ μλ‘μ΄ μμκ° λ€μ΄μ€λ©΄, μΌλ¨ μλ‘μ΄ λΈλλ₯Ό ννμ λ§μ§λ§ λΈλμ μ΄μ΄μ μ½μνλ€.
2 μ½μ νμ μλ‘μ΄ λΈλλ₯Ό λΆλͺ¨ λΈλλ€κ³Ό κ΅νν΄μ ννμ μ±μ§μ λ§μ‘±μν¨λ€.

### ππ»upheap μ°μ°
 ![](/Images/upheap.JPG)

- **μκ³ λ¦¬μ¦**
    ```
    1. νν ν¬κΈ°λ₯Ό νλ μ¦κ°μν¨λ€.
    2. μ¦κ°λ νν ν¬κΈ° μμΉμ μλ‘μ΄ λΈλλ₯Ό μ½μνλ€.
    3. iκ° λ£¨νΈ λΈλκ° μλκ³ , iλ²μ§Έ λΈλκ° iμ λΆλͺ¨λΈλλ³΄λ€ ν¬λ©΄ iλ²μ§Έ λΈλμ λΆλͺ¨ λΈλλ₯Ό κ΅ν
    4. iλ²μ§Έ λΈλμ λΆλͺ¨ λΈλλ₯Ό κ΅ν
    5. ν λ λ²¨ μλ‘ μ¬λΌκ°λ€. (μΉμ§)
    ```
    ```C
    void insert_min_heap(HeapType* h, element item) {
        int i;
        i = ++(h->heap_size);
        while (i != 1 && (item.key > h->heap[i / 2].key)) {
            h->heap[i] = h->heap[i / 2];
            i /= 2;
        }
        h->heap[i] = item; //μλ¦¬μ item λ£κΈ°
    }
    ```

### ππ»νν μ­μ 
: μ¬μ₯μ μλ¦¬κ° λΉκ²λλ©΄ λ¨Όμ  μ μΌ λ§λ¨ μ¬μμ μ¬μ₯ μλ¦¬λ‘ μν λ€μ, λ₯λ ₯μ λ°λΌ κ°λ±μν¨λ€.
1. λ£¨νΈ λΈλλ₯Ό μ­μ νλ€.
2. λ§μ§λ§ λΈλλ₯Ό λ£¨νΈ λΈλλ‘ μ΄λνλ€.
3. λ£¨νΈμμλΆν° λ¨λ§ λΈλκΉμ§μ κ²½λ‘μ μλ λΈλλ€μ κ΅ννμ¬ νν μ±μ§μ λ§μ‘±μν¨λ€.

### ππ»downheap μ°μ°
 ![](/Images/downheap.JPG)

 - **μκ³ λ¦¬μ¦**
    ```
    1. λ£¨νΈ λΈλ κ°μ λ°νμ μνμ¬ item λ³μλ‘ μ?κΈ΄λ€.
    2. λ§λ¨ λΈλλ₯Ό λ£¨νΈ λΈλλ‘ μ?κΈ΄λ€.
    3. ννμ ν¬κΈ°λ₯Ό νλ μ€μΈλ€.
    4. λ£¨νΈμ μΌμͺ½ μμλΆν° λΉκ΅λ₯Ό μμνλ€.
    5. iκ° νν νΈλ¦¬μ ν¬κΈ°λ³΄λ€ μμΌλ©΄(μ¦, νννΈλ¦¬λ₯Ό λ²μ΄λμ§ μμΌλ©΄)
    6. μ€λ₯Έμͺ½ μμμ΄ λ ν¬λ©΄
    7-8. λκ°μ μμλΈλ δΈ­ ν° κ°μ μΈλ±μ€λ₯Ό largestλ‘ μ?κΈ΄λ€.
    9. largestμ λΆλͺ¨λΈλκ° largestλ³΄λ€ ν¬λ©΄
    10. μ€μ§
    11. κ·Έλ μ§ μμΌλ©΄, largestμ largest λΆλͺ¨λΈλλ₯Ό κ΅ννλ€.
    12. ν λ λ²¨ λ°μΌλ‘ λ΄λ €κ°λ€.
    13. μ΅λ κ°μ λ°ννλ€.
    ```
    ```C
    element delete_max_heap(HeapType* h) {
        int parent, child;
        element item, temp;

        item = h->heap[1];
        temp = h->heap[(h->heap_size)--]; //μ μΌ λ§λ¨ λΈλ
        parent = 1;
        child = 2;
        while (child <= h->heap_size) {
            if(child < h->heap_size && (h->heap[child].key < h->heap[child + 1].key))
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
    ```

### π»heap skeleton
<details markdown="1">
<summary>max_heap μ½λ λ³΄κΈ°π</summary>

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
	h->heap[i] = item; //μλ¦¬μ item λ£κΈ°
}

element delete_max_heap(HeapType* h) {
	int parent, child;
	element item, temp;

	item = h->heap[1];
	temp = h->heap[(h->heap_size)--]; //μ μΌ λ§λ¨ λΈλ
	parent = 1;
	child = 2;
	while (child <= h->heap_size) {
		if(child < h->heap_size && (h->heap[child].key < h->heap[child + 1].key))
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
int main(void)
{
	element e1 = { 10 }, e2 = { 5 }, e3 = { 30 };
	element e4, e5, e6;
	HeapType* heap;
	heap = create(); // νν μμ±
	init(heap); // μ΄κΈ°ν
	// μ½μ
	insert_max_heap(heap, e1);
	insert_max_heap(heap, e2);
	insert_max_heap(heap, e3);
	// μ­μ 
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

### ππ»λ³΅μ‘λ λΆμ 
- `μ½μ` : μ΅μμ κ²½μ°, λ£¨νΈ λΈλκΉμ§ μ¬λΌκ°μΌ νλ―λ‘ νΈλ¦¬μ λμ΄μ ν΄λΉνλ λΉκ΅μ°μ° λ° μ΄λμ°μ° νμ!
    - **O(logn)**

- `μ­μ ` : μ΅μμ κ²½μ°, κ°μ₯ μλ λ λ²¨κΉμ§ λ΄λ €κ°μΌνλ―λ‘ μ­μ νΈλ¦¬μ λμ΄λ§νΌμ μκ°μ΄ κ±Έλ¦°λ€.
    - **O(logn)**

---
</br>



