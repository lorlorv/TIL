# π»μ€λ λ μ΄μ§νΈλ¦¬ 
: μ΄μ§νΈλ¦¬μ NULLλ§ν¬λ₯Ό μ΄μ©νμ¬ μννΈμΆ μμ΄λ νΈλ¦¬μ λΈλλ€μ μν
- νΈλ¦¬ λΈλμ κ°μκ° nκ°μΌ λ μ΄ λ§ν¬μ κ°μλ 2n
- 2nκ° δΈ­ n-1μ NULL λ§ν¬κ° μλμ§λ§ **λλ¨Έμ§ n+1κ°μ λ§ν¬λ NULL!**

: NULL λ§ν¬μ μ€μ μνμμ νμ λΈλμΈ μ€μ νμμ(indorder successor)λ₯Ό μ μ₯μμΌλμ νΈλ¦¬

### γ **μ€λ λ μ΄μ§ νΈλ¦¬ (Threaded Binary Tree)**

#### `μν`
- inorder
    - μ¬κ·(μ€ν λ¬΅μμ )
    - λ°λ³΅ μ΄μ©(μ€ν λͺμμ )
    - μ€λ λ μ΄μ§ νΈλ¦¬

![](/Images/μ€λ λμ΄μ§νΈλ¦¬1.JPG)

---
</br>

## κ΅¬ν
### `is_thread` </br>
: μ€λ₯Έμͺ½ νλκ° μκΈ° μμ μ κ°λ¦¬ν€λ κ²½μ° / μ€μ νμμλ₯Ό κ°λ¦¬ν€λ κ²½μ°λ₯Ό κ΅¬λ³νκΈ° μνμ¬ is_thread ν¨μκ° νμνλ€. </br>

![](/Images/is_thread.JPG)

### **β΄ is_threadμ κ°**
- TRUE : right == μ€μ νμμ
- FALSE : right == μ€λ₯Έμͺ½ μμμ κ°λ¦¬ν€λ ν¬μΈν°

### `TreeNode *find_successor(TreeNode *p)` </br>
: μ€μ νμμλ₯Ό λ°ννλ ν¨μ </br>
1. pμ is_threadμ κ°
    - TRUE : λ°λ‘ μ€λ₯Έμͺ½ μμμ΄ μ€μ νμμκ° λλ―λ‘ μ€λ₯Έμͺ½ μμμ λ°ν
    - !TRUE : μλΈ νΈλ¦¬μ κ°μ₯ μΌμͺ½ λΈλλ‘ κ°μΌνλ€.
2. λ§μ½, μ€λ₯Έμͺ½ μμμ΄ NULLμ΄λ©΄ λ μ΄μ νμμκ° μμΌλ―λ‘ NULL λ°ν

![](/Images/find_successor.JPG)


### `void thread_inorder (TreeNode *t)` </br>
1. μΌμͺ½ μμμ΄ NULLμ΄ λ  λκΉμ§ μΌμͺ½ λ§ν¬λ₯Ό νκ³  μ΄λνλ€.
2. λ°μ΄ν°λ₯Ό μΆλ ₯
3. μ€μ νμμλ₯Ό μ°Ύλ ν¨μλ₯Ό νΈμΆνκ³  νμμκ° NULLμ΄ μλ λμ λ°λ³΅νλ€.

---
</br>

### `μ₯μ ` : μνλ₯Ό λΉ λ₯΄κ² ν  μ μλ€.
### `λ¨μ ` : μ€λ λλ₯Ό μ€μ νκΈ° μνμ¬ μ½μμ΄λ μ­μ  ν¨μκ° λ λ§μ μΌμ ν΄μΌνλ€.

---
</br>

## π»Skeleton
```C
//μ€λ λ μ΄μ§ νΈλ¦¬
#include <stdio.h>
typedef int element;
typedef struct TreeNode {
	element data;
	struct TreeNode* left, *right;
	element is_thread;
}TreeNode;

//μ€μ νμμλ₯Ό λ°ννλ ν¨μ 
TreeNode* find_successor(TreeNode* p) {
	TreeNode* q = p->right;
	if (q == NULL || p->is_thread == 1)
		return q;

	//λ§μ½ μ€λ₯Έμͺ½ μμμ΄λ©΄ λ€μ κ°μ₯ μΌμͺ½ λΈλλ‘ μ΄λ
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
	} while (q); //νμμκ° NULLμ΄ μλλκΉμ§
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
	//μ€λ λ μ€μ 
	n1.right = &n2;
	n2.right = &n7;
	n3.right = &n4;
	n4.right = &n6;

	//μ€μ μν
	thread_inorder(root);
	printf("\n");
	return 0;
}
```

