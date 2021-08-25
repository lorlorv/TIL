# Priority Queue
## 선언
### import java.util.PriorityQueue;
1. int형 pq선언 (우선순위가 낮은 순)
    ```Java
    PriorityQueue <Integer> pq = new PriorityQueue<>();
    ```
2. int형 pq선언 (우선순위가 높은 순)
    ```Java
    PriorityQueue <Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
    ```
3. String형 pq선언 (우선순위가 낮은 순)
    ```Java
    PriorityQueue <Integer> pq = new PriorityQueue<>();
    ```
4. String형 pq선언 (우선순위가 높은 순)
    ```Java
    PriorityQueue <Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
    ```

## 값 추가
- `add(value)` 
    - 성공 → true;
    - 실패 → IllegalStateException
- `offer(value)`

## 값 삭제
- `poll()` : 첫번째 값을 반환하고 제거, 비어있다면 null
- `remove()` : 첫번째 값 제거
- `clear()` : 모든 요소를 제거, 초기화

## 참조
- `peek()` : 첫번째 값 반환
- `element()` : 첫번째 값 반환, 큐가 비어있다면 예외 발생

## Comparable
PriorityQueue를 사용하기 위해서 우선순위에 저장할 객체는 필수적으로 **Comparable Interface**를 구현해야한다.

- 구현 후 
    - **compareTo 메소드** override <br>
    → 해당 객체에서 처리 할 우선순위 조건을 return 해주면 </br>
    → pq가 알아서 우선순위가 높은 객체를 추출해준다.

자세한 내용은 [객체 정렬하기 Comparable&Comparator](/Study/JAVA/Comparable&Comparator.md)