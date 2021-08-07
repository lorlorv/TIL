# 완전탐색(Brute Force)

- 컴퓨터의 빠른 계산 능력을 이용하여 가능한 경우의 수를 일일이 나열하며 답을 찾는 방법
- Brute Force 라고도 부르는데, 뜻은 무식하게 푼다!
- 완전탐색은 알고리즘이 아닌, **문제를 푸는 방법**이라고 할 수 있다.
</br>

---

</br>

> 완전 탐색 기법 </br>

`1. 단순 Brute Force`
- if문이나 for문을 사용해 모든 case를 탐색하는 방법 

`2. Bit-mask`
- 모든 경우의 수가 각각의 원소에 포함되거나 포함되지 않는 **두 가지 선택**으로 구성되는 경우 용이하다.
- 이를 통해 집합을 정수로 나타내거나 집합의 모든 부분집합을 정수로 표현할 수 있다.

```
{1, 2, 3, 4, 5} -> 1 1 1 1 1 -> 31
{1, 2, 3, 4}    -> 1 1 1 1 0
{2, 3, 5}       -> 0 1 1 0 1
{3, 4}          -> 0 0 1 1 0
{1}             -> 1 0 0 0 0

: 모든 원소가 있는 부분집합 == 31
```
- 만약, 해당 부분집합에 i를 추가하고 싶다면 i번째 비트를 1로 바꿔주면 됨 
    - 이때 비트연산을 활용!
        - AND OR XOR NOT SHIFT

`3. 백 트래킹`
- 완전 탐색 도중 해가 되지 않을 것 같은 경로가 있다면 진행하지 않고 back한다.

`4. 재귀` </br>
`5. 순열`
- for문 사용
    - 수가 적을 때 사용한다.
- 재귀 
    ```C
    int n = 4, r = 3; //4개 중에서 3개 뽑기
    int check[4]; 
    int result[3]; //결과를 담을 배열
    int arr[] = { 1,2,3,4 };
    ```
    ```C
    void permutation(int idx) { //순열
        if (idx == r) {
            for (int i = 0; i < r; i++) {
                printf("%d", result[i]);
            }
            printf("\n");
            return;
        }

        for (int i = 0; i < n; i++) {
            if (check[i] != 1) {
                result[idx] = arr[i];
                check[i] = 1; // TRUE
                permutation(idx + 1);
                check[i] = 0; //FALSE
            }
        }
    }
    ```

`5. BFS/DFS`
</br>
### ✏순열


- 뽑는 아이템의 순서가 중요하다! 
- 123 132 231 ...  = 다 다른 친구들

```C
#include<stdio.h>

int n = 4, r = 3; //4개 중에서 3개 뽑기
int check[4]; 
int result[3]; //결과를 담을 배열
int arr[] = { 1,2,3,4 };

void permutation(int idx) { //순열
	if (idx == r) {
		for (int i = 0; i < r; i++) {
			printf("%d", result[i]);
		}
		printf("\n");
		return;
	}

	for (int i = 0; i < n; i++) {
		if (check[i] != 1) {
			result[idx] = arr[i];
			check[i] = 1; // TRUE
			permutation(idx + 1);
			check[i] = 0; //FALSE
		}
	}
}
int main(void) {
	permutation(0);
}
```
- `check` :  특정 수가 뽑혔는 지 안 뽑혔는 지 확인 
- `result` : 결과를 담아 출력 시 활용할 배열 
- `idx` : 뽑아야 할 자리의 index
- `permutation 함수` : 
	 - check[i]의 자리를 검사! 
	 	- -> TRUE 가 아니면 result[idx]에 arr[i]의 값을 넣어주고 check를 TRUE로 바꿔주기.
			- 다음 자리에 수를 넣기위해 idx + 1로 재귀 수행!
		- -> TRUE 라면 다음 check값으로 넘어간다.

	- idx와 뽑아야 할 개수인 r이 같다면 
		- 지금까지 모았던 result를 출력해준다.
	- 재귀를 다 수행했다면 백 트래킹으로 check[i]값을 FALSE로 바꿔주고 다른 수를 넣어준다.
	 

___
</br>

### 📎브루트포스/DFS/백트래킹을 이용한 문제
`백준 14888`

```C
#include <stdio.h>
#define MAX 1000000000 + 1
#define MIN -(1000000000 + 1)

int N;
int sum = 0, max = MIN, min = MAX;
int arr[12];
int operator[4];

void calc(int index, int sum) {//index == 1, sum == arr[0]

	//연산자 다 썼으면 MAX인지 MIN인지 판별
	if (index == N) {
		if (max < sum) max = sum;
		if (min > sum) min = sum;

		return;
	}

	for (int i = 0; i < 4; i++) {
		if (operator[i]) { //operator[i]가 0이 아닐동안
			operator[i]--; //한번 썼으니까
			if (i == 0)
				calc(index + 1, sum + arr[index]);
			else if (i == 1)
				calc(index + 1, sum - arr[index]);
			else if (i == 2)
				calc(index + 1, sum * arr[index]);
			else
				calc(index + 1, sum / arr[index]);

			//백트래킹으로 다른 연산자를 넣어준다
			operator[i]++;
		}	
	}	
}

int main(void) {
	int number;
	int count;

	scanf_s("%d", &N);

	for (int i = 0; i < N; i++) {
		scanf_s("%d", &number);
		arr[i] = number;
	}

	for (int i = 0; i < 4; i++) { //+, - , *, / 가 각각 몇개씩 있는 지 ex) 2112
		scanf_s("%d", &count); 
		operator[i] = count;
	}
	calc(1, arr[0]);
	printf("%d\n%d", max, min);
}
```
- 모든 경우의 수를 다 따져보아야한다는 점
-> **브루트포스**!
- 한번 완성되었던 연산자 모음을 피하기 위해 **백트래킹**을 이용하여 다른 연산자를 넣어 다른 연산자 모음을 만든다.
- 하나의 연산자를 다 사용할 때까지 **DFS** 알고리즘을 이용하여 연산자 모음을 만들어간다.
