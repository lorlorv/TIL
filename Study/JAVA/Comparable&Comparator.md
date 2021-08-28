# 객체 정렬하기 Comparable & Comparator 🍻
: 둘 다 Interface → 메소드 반드시 구현해야함!

### [comparable](#comparable)
: 자기 자신과 매개변수 객체 비교 

### [comparator](#comparator)
: 두 매개변수 객체를 비교 

### `차이점` : **비교대상**

---
## Comparable
### **정의** 
: 정렬 수행 시 기본적으로 적용되는 정렬 기준이 되는 메소드를 정의하는 인터페이스 
package : `java.lang.Comparable`

### **구현방법**
- 정렬할 객체에 `Comparable Interface`를 implements한다.
- **` compareTo()`** method override
1.
    - 현재 객체 < 파라미터로 넘어온 객체 : *return 음수*
    - 현재 객체 == 파라미터로 넘어온 객체 : *return 0*
    - 현재 객체 > 파라미터로 넘어온 객체 : *return 양수*
    
        - `음수 or 0` → 객체 자리 유지
        - `양수` → 두 객체의 자리 change

2. if, elseif, else 대신 **`Integer.compare()`** method 사용가능
    - x == y → 0
    - x < y → 음수
    - x > y → 양수

3. **`현재 객체 - 파라미터`** 로 넘어온 객체의 값으로 값 판별
    - `return this.age - o.age`
    - **주의할 점** : 뺄셈과정에서 자료형의 범위를 넘어 버리는 경우!
        ```Java
        int x = Integer.MAX_VALUE; //2,147,483,647
        int y = Integer.MIN_VALUE; //-2,147,483,648
        ```
    -  y - 1 == -2,147,483,648 - 1 == -2,147,483,649
        - Integer.MIN_VALUE 값을 넘어버리므로 **int형의 최댓값으로 반환한다.** </br> *=> Underflow*
            - 주어진 범위의 하한선을 넘어버리는 것
    -  x + 1 == 2,147,483,647 + 1 == -2,147,483,648
        - Integer.MAX_VALUE 값을 넘어버리므로 **int형의 최솟값으로 반환한다.** </br> *=> Overflow*
            - 주어진 범위의 상한선을 넘어버리는 것

        👀 if ) o1 = 1, o2 = -2,147,483,647 </br>
        
        - o1 - o2를 했을 때 2,147,483,648 이 되어야 하지만 **Overflow가 발생**해 -2,147,483,648가 되어 음수값이 나와버린다. 그렇다면, o1이 o2보다 작다는 상황이 일어난다.
    - 👉 Overflow or Underflow가 발생하지 않는 지 체크하고 사용하기!

### **사용방법**
- Arrays.sort(array)
- Collections.sort(list)

---

## Comparator
### **정의**
: 정렬 가능한 클래스 (Comparable Interface를 구현한 클래스)들의 기본 정렬 기준과 다르게 정렬하고 싶을 때 사용하는 인터페이스 </br>
package : java.util.Comparator

- 주로 익명 클래스로 사용된다.
- 기본적인 정렬 방법인 오름차순 정렬을 내림차순으로 정렬할 때 많이 사용된다.

### **구현방법**
1. Comparable Interface implements
2. compare() method를 override한 myComparator class 작성
    - 첫 번째 파라미터로 넘어온 객체 < 두 번째 파라미터로 넘어온 객체 : *return 음수*
    - 첫 번째 파라미터로 넘어온 객체 == 두 번째 파라미터로 넘어온 객체 : *return 0*
    - 첫 번째 파라미터로 넘어온 객체 > 두 번째 파라미터로 넘어온 객체 : *return 양수*

        - `음수 or 0` → 객체 자리 유지
        - `양수` → 두 객체의 자리 change

### **사용방법**
- Arrays.sort(array, myComparator)
- Collections.sort(list, myComparator) </br>

Arrays.sort(), Collections.sort() 메소드는 **두 번째 인자로 Comparator interface를 받을 수 있다.**
```Java
public static <T> void sort (T[] a, Comparator <?superT> c)
```
- Comparator 파라미터로 넘어온 c의 비교 기준을 가지고 파라미터로 넘어온 객체 
### 👉🏻 우선순위 큐(Priority Queue)
- 지정된 Comparator의 정렬 방법에 따라 우선 순위를 할당

---
## 활용
💡 comparator 비교 기능만 따로 두고 싶을 때 </br>
=> **익명 클래스 사용** : 이름이 정의 되지 않은 객체 
- 반드시 익명 객체는 상속할 대상이 있어야한다. </br>
→ Comparator 라는 Interface가 존재하기 때문에 상속할 대상이 존재하며 즉, 익명 객체로 만들 수 있다.

ex) 
```Java
public static Comparator<클래스 이름> comp1 = new Comparator<클래스 이름>(){
    public int compare(객체 1, 객체 2)

              ~

};
```
### ∴ 클래스 내부에서 Comparator 구현 필요 ❌
- a.compare(b, c) (❌)
- comp1.compare(b, c) (⭕)
