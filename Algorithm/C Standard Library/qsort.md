# ✏ qsort

## 원형
-  `void qsort(void *base, size_t num, size_t width, int (*compare)(const void *key, const void *element))` 

## 필요헤더
- stdlib.h

## 매개변수
1. `void *base` : 정렬할 배열
2. `size_t num` : 배열의 총 element 개수 (=배열의 크기)
3. `size_t width` : 배열 한 개의 크기 (=요소의 크기)
4. `compare` : 비교를 수행할 함수의 포인터
    - 반환되는 값에 따라 내림차순 or 오름차순이 결정된다.
        - 오름차순 
            |비교|값|
            |:---:|:---:|
            |a > b | 1|
            |a < b | -1|
            |a == b| 0|
        
        - 내림차순 
            |비교|값|
            |:---:|:---:|
            |a < b | 1|
            |a > b | -1|
            |a == b| 0|
        
    - 함수 포인터인 이유 : **call back**
        - 어떤 데이터 타입이라도 처리할 수 있도록 하기 위함이다.
            - 함수 작성 시 **형변환**해서 비교해야 함!
    - 문자열이라면 compare 함수에 strcmp를 넣어 똑같이 값을 return한다.  

*.`void *` : 정해지지 않은 타입을 표현 int, char 등 다양하게 들어올 수 있다.

</br>

___


## 💻 코드구현

- `정수 정렬`
```C
#include <stdio.h>
#include <stdlib.h>

//오름차순
int compare_int_up(const void* a, const void* b) {
	if (*(int*)a > *(int*)b)
		return 1;
	else if (*(int*)a < *(int*)b)
		return -1;
	else
		return 0;
}
//내림차순
int compare_int_down(const void* a, const void* b) {
	if (*(int*)a < *(int*)b)
		return 1;
	else if (*(int*)a > *(int*)b)
		return -1;
	else
		return 0;
}

int main(void) {
	int arr[] = { 5,8,2,3,10,4,7,9,6,1 };

	for (int i = 0; i < 10; i++) {
		printf("%d ", arr[i]);
	}

	qsort(arr, 10, sizeof(arr[0]), compare_int_up);

	printf("\n오름차순 :");
	for (int i = 0; i < 10; i++) {
		printf("%d ", arr[i]);
	}

	qsort(arr, 10, sizeof(arr[0]), compare_int_down);

	printf("\n내림차순 :");
	for (int i = 0; i < 10; i++) {
		printf("%d ", arr[i]);
	}

	return 0;
}
```

- `문자열 정렬`
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

//오름차순
int compare_string_up(const void* a, const void* b) {
	return strcmp((char*)a, (char*)b);
}
//내림차순
int compare_string_down(const void* a, const void* b) {
	return strcmp((char*)b, (char*)a);
}

int main(void) {
	char arr[][10] = { "elephant", "choco", "atom", "banana", "dinosour"};

	for (int i = 0; i < 5; i++) {
		printf("%s ", arr[i]);
	}

	qsort(arr, 5, sizeof(*arr), compare_string_up);

	printf("\n오름차순 :");
	for (int i = 0; i < 5; i++) {
		printf("%s ", arr[i]);
	}

	qsort(arr, 5, sizeof(*arr), compare_string_down);

	printf("\n내림차순 :");
	for (int i = 0; i < 5; i++) {
		printf("%s ", arr[i]);
	}

	return 0;
}
```
