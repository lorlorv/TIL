# 👻스레드 이진트리 
: 이진트리의 NULL링크를 이용하여 순환호출 없이도 트리의 노드들을 순회
- 트리 노드의 개수가 n개일 때 총 링크의 개수는 2n
- 2n개 中 n-1은 NULL 링크가 아니지만 **나머지 n+1개의 링크는 NULL!**

: NULL 링크에 중위 순회시에 후속 노드인 중위 후속자(indorder successor)를 저장시켜놓은 트리

### 〓 **스레드 이진 트리 (Threaded Binary Tree)**

#### `순회`
- inorder
    - 재귀(스택 묵시적)
    - 반복 이용(스택 명시적)
    - 스레드 이진 트리

![](/Images/스레드이진트리1.JPG)

---
</br>

## 구현
### `is_thread` </br>
: 오른쪽 필드가 자기 자신을 가리키는 경우 / 중위 후속자를 가리키는 경우를 구별하기 위하여 is_thread 함수가 필요하다. </br>

![](/Images/is_thread.JPG)

### **∴ is_thread의 값**
- TRUE : right == 중위 후속자
- FALSE : right == 오른쪽 자식을 가리키는 포인터

### `TreeNode *find_successor(TreeNode *p)` </br>
: 중위 후속자를 반환하는 함수 </br>
1. p의 is_thread의 값
    - TRUE : 바로 오른쪽 자식이 중위 후속자가 되므로 오른쪽 자식을 반환
    - !TRUE : 서브 트리의 가장 왼쪽 노드로 가야한다.
2. 만약, 오른쪽 자식이 NULL이면 더 이상 후속자가 없으므로 NULL 반환

![](/Images/find_successor.JPG)


### `void thread_inorder (TreeNode *t)` </br>
1. 왼쪽 자식이 NULL이 될 때까지 왼쪽 링크를 타고 이동한다.
2. 데이터를 출력
3. 중위 후속자를 찾는 함수를 호출하고 후속자가 NULL이 아닌 동안 반복한다.

---
</br>

### `장점` : 순회를 빠르게 할 수 있다.
### `단점` : 스레드를 설정하기 위하여 삽입이나 삭제 함수가 더 많은 일을 해야한다.

---
</br>

## 💻Skeleton
```C
//스레드 이진 트리
#include <stdio.h>
typedef int element;
typedef struct TreeNode {
	element data;
	struct TreeNode* left, *right;
	element is_thread;
}TreeNode;

//중위 후속자를 반환하는 함수 
TreeNode* find_successor(TreeNode* p) {
	TreeNode* q = p->right;
	if (q == NULL || p->is_thread == 1)
		return q;

	//만약 오른쪽 자식이면 다시 가장 왼쪽 노드로 이동
	while (q->left != NULL) q = q->left;
	return q;
}

void thread_inorder(TreeNode* t) {
	TreeNode* q;
	q = t;
	while (q->left != NULL) q = q->left;
	do {
		printf("%d->", q->data);
		q = find_successor(q);
	} while (q); //후속자가 NULL이 아닐때까지
}

//      7
//   3     6
// 1     4   8
//     5

TreeNode n1 = { 1, NULL, NULL,1 };
TreeNode n2 = { 3, &n1, NULL,1 };
TreeNode n3 = { 5, NULL, NULL ,1};
TreeNode n4 = { 4, &n3, NULL,1 };
TreeNode n5 = { 8, NULL, NULL,0 };
TreeNode n6 = { 6, &n4, &n5 ,0};
TreeNode n7 = { 7, &n2, &n6 ,0};
TreeNode* root = &n7;

int main(void) {
	//스레드 설정
	n1.right = &n2;
	n2.right = &n7;
	n3.right = &n4;
	n4.right = &n6;

	//중위 순회
	thread_inorder(root);
	printf("\n");
	return 0;
}
```

