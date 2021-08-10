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



