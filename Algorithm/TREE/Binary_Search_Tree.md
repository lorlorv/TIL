# π₯Binary Search Tree
## μ΄μ§ νμ νΈλ¦¬ 
: νμμμμ ν¨μ¨μ μΌλ‘ νκΈ° μν μλ£κ΅¬μ‘° 

## μ μ
1. λͺ¨λ  μμμ ν€λ μ μΌν ν€λ₯Ό κ°μ§λ€.
2. μΌμͺ½ μλΈνΈλ¦¬ ν€λ€μ λ£¨νΈμ ν€λ³΄λ€ μλ€.
3. μ€λ₯Έμͺ½ μλΈ νΈλ¦¬μ ν€λ€μ λ£¨νΈμ ν€λ³΄λ€ ν¬λ€.
4. μΌμͺ½κ³Ό μ€λ₯Έμͺ½ μλΈνΈλ¦¬λ μ΄μ§ νμ νΈλ¦¬μ΄λ€.

**: μ΄μ§ νμμ μ€μ μννλ©΄ μ€λ¦μ°¨μμΌλ‘ μ λ ¬λ κ°μ μ»μ μ μλ€.**

---
</br>

## νμ κ΅¬ν
- λ°λ³΅μ  λ°©λ²
- μνμ  λ°©λ²

### `μνμ μΈ νμ μ°μ°`
: λ£¨νΈ λΈλμ ν€ κ°κ³Ό μ£Όμ΄μ§ νμ ν€ κ°μ λΉκ΅ν κ²°κ³Όκ°
1. κ°μΌλ©΄ νμμ΄ μ±κ³΅μ μΌλ‘ λλλ€.
2. μ£Όμ΄μ§ ν€ κ°μ΄ λ£¨νΈλΈλμ ν€ κ°λ³΄λ€ μμΌλ©΄ νμμ μ΄ λ£¨νΈ λΈλμ μΌμͺ½ μμμ κΈ°μ€μΌλ‘ λ€μ μμνλ€.
3. μ£Όμ΄μ§ ν€ κ°μ΄ λ£¨νΈλΈλμ ν€ κ°λ³΄λ€ ν¬λ©΄ νμμ μ΄ λ£¨νΈ λΈλμ μ€λ₯Έμͺ½ μμμ κΈ°μ€μΌλ‘ λ€μ μμνλ€.

### `μνμ  μκ³ λ¦¬μ¦`
```C
Treenode *search (TreeNode *node, int key){
    if(node == NULL) return NULL;
    if(node β key == key) return node;
    else if(key < node β key)
        return search(node β left, key);
    else
        return search(node β right, key);
}
```

### `λ°λ³΅μ  μκ³ λ¦¬μ¦`
```C
TreeNode *search (TreeNode *node, int key){
    while(node != NULL){
        if(key == node β key) return node;
        else if(key < node β key)
            node = node β left;
        else
            node = node β right;
    }
    return NULL;
}
```
## μ½μ μ°μ°
: λ¨Όμ  νμ μν νμ! </br>
### **`μ΄μ `** 
1. κ°μ ν€ κ°μ κ°λ λΈλ μμ΄μΌ ν¨
2. νμμ μ€ν¨ν μμΉκ° μ½μνλ μμΉ!

    ![](/Images/insert_bst.JPG)

### **`μκ³ λ¦¬μ¦`**
```C
TreeNode *insert(TreeNode *node, int key){
    if(node == NULL) return NULL;
    if(key < node β key )
        node β left = insert(node β left, key);
    else if(key > node β key)
        node β right = insert(node β right, key);
    
    return node;
}
```
## μ­μ  μ°μ°
: κ³ λ €μ¬ν­
1. μ­μ νλ €λ λΈλκ° λ¨λ§λΈλμΌ κ²½μ°
2. μ­μ νλ €λ λΈλκ° νλμ μΌμͺ½μ΄λ μ€λ₯Έμͺ½ μλΈνΈλ¦¬λ§μ κ°μ§κ³  μλ κ²½μ°
3. μ­μ νλ €λ λΈλκ° λκ°μ μλΈνΈλ¦¬ λͺ¨λ κ°μ§κ³  μλ κ²½μ°

![](/Images/delete_3case.JPG)
- case 1
    - λ¨λ§λΈλ μ­μ , λΆλͺ¨λΈλ λ§ν¬ NULL
- case 2
    - λΈλ μ­μ , μλΈ νΈλ¦¬λ λΆλͺ¨λΈλμ λΆμ΄κΈ°
- case 3
    - μ­μ λΈλμ κ°μ₯ λΉμ·ν κ° λΈλλ₯Ό μ­μ  λΈλ μμΉλ‘
        - **κ°μ₯ λΉμ·ν κ° λΈλλ μ΄λμ μμκΉ?** </br>
            1. μΌμͺ½ μλΈνΈλ¦¬μμ κ°μ₯ ν° κ°
            2. μ€λ₯Έμͺ½ μλΈ νΈλ¦¬μμ κ°μ₯ μμ κ°

### `μκ³ λ¦¬μ¦`
```C
    //case 1, 2 :
    if(root β left == NULL){
        TreeNode *temp = root β right;
        free(root);
        return temp;
    }

    else if(root β right == NULL){
        TreeNode *temp = root β left;
        free(root);
        return temp;
    }
    //case 3:
    TreeNode *temp = min_value_node(root β right);
    root β key = temp β key;
    root β right = delete_node(root β right, temp β key);

```
### π»BST skeleton
<details markdown="1">
<summary>BST μ½λ λ³΄κΈ°π</summary>

```C
//μ΄μ§ νμ νΈλ¦¬
#include <stdio.h>
#include <stdlib.h>

#define MAX(a,b) ((a > b) ? a : b)
#define MIN(a,b) ((a < b) ? a : b)

typedef int element;
typedef struct TreeNode{
	element data;
	struct TreeNode* left, *right;
}TreeNode;

TreeNode* newNode(int item) {
	TreeNode* temp = (TreeNode*)malloc(sizeof(TreeNode));
	temp->data = item;
	temp->left = temp->right = NULL;
	return temp;
}

TreeNode* insert(TreeNode* t, int key) {
	if (t == NULL) return newNode(key);

	if (key < t->data)
		t->left = insert(t->left, key);
	else if (key > t->data)
		t->right = insert(t->right, key);

	return t;
}
TreeNode* get_Min(TreeNode* t) {
	TreeNode* temp = t;
	while (temp->left != NULL) temp = temp->left;
	return temp;
}
TreeNode* delete(TreeNode* t, int key) {
	TreeNode* temp;

	if (t == NULL)return NULL;

	if (key < t->data)
		t->left = delete(t->left, key);
	else if (key > t->data)
		t->right = delete(t->right, key);
	else { //μ­μ ν  keyλ₯Ό μ°ΎμμΌλ μ§μ§ μ­μ  μμ!
		//case 1, 2
		if (t->left == NULL) {
			TreeNode* temp = t->right;
			free(t);
			return temp;
		}
		else if (t->right == NULL) {
			TreeNode* temp = t->left;
			free(t);
			return temp;
		}
		//case 3
		TreeNode* temp = get_Min(t->right);
		t->data = temp->data;
		t->right = delete(t->right, temp->data);
	}
	return t;
}
TreeNode* search(TreeNode* t, int key) {
	if (t == NULL)return NULL;
	if (t->data == key)
		return t;
	else if (key < t->data)
		return  search(t->left, key);
	else
		return search(t->right, key);
}

void preorder_print(TreeNode* t) {
	if (t != NULL) {		
		printf("[%d] ", t->data);
		preorder_print(t->left);
		preorder_print(t->right);
	}
}
int get_height(TreeNode* t) {
	int height;

	if (t == NULL)return 0;
	if (t != NULL) {
		height = 1 + MAX(get_height(t->left), get_height(t->right));
	}
	return height;
}

int node_count(TreeNode* t) {
	int cnt = 0;
	if (t == NULL) return 0;
	if (t != NULL) {
		cnt = 1 + node_count(t->left) + node_count(t->right);
	}
	return cnt;
}

int main(void) {
	TreeNode* root = NULL;

	root = insert(root, 30);
	root = insert(root, 20);
	root = insert(root, 10);
	root = insert(root, 40);
	root = insert(root, 50);
	root = insert(root, 60);

	printf("μ΄μ§ νμ νΈλ¦¬ μ μ μν κ²°κ³Ό \n");
	preorder_print(root);
	printf("\n\n");
	printf("μ΄μ§ νμ νΈλ¦¬μ λμ΄ : %d\n", get_height(root));
	printf("μ΄μ§ νμ νΈλ¦¬μ λΈλ κ°μ : %d\n", node_count(root));
	printf("\n");

	printf("-----------------------------------------\n\n");

	if (search(root, 30) != NULL)
		printf("μ΄μ§ νμ νΈλ¦¬μμ 30μ λ°κ²¬ν¨ \n");
	else
		printf("μ΄μ§ νμ νΈλ¦¬μμ 30μ λ°κ²¬νμ§ λͺ»ν¨ \n");

	printf("\n-----------------------------------------\n");

	root = delete(root, 20);
	printf("\nμ΄μ§ νμνΈλ¦¬μμ 20μ μ­μ \n");
	preorder_print(root);
	printf("\n\n");

	printf("μ΄μ§ νμ νΈλ¦¬μ λμ΄ : %d\n", get_height(root));
	printf("μ΄μ§ νμ νΈλ¦¬μ λΈλ κ°μ : %d\n", node_count(root));

	return 0;
}
```
</details>

---
</br>


## μ±λ₯ λΆμ
νμ, μ½μ, μ­μ  μ°μ°μ μκ°λ³΅μ‘λ
### : **λμ΄ hμ λΉλ‘**

- `μ΅μ ` : μ΄μ§νΈλ¦¬κ° κ· νμ μΌλ‘ μμ±λμ΄ μλ κ²½μ° 
    - **h = logβββΏ**
    
- `μ΅μ` : ν μͺ½μΌλ‘ μΉμ°μΉ κ²½μ¬ μ΄μ§ νΈλ¦¬ 
    - h = n
    - μμ°¨ νμκ³Ό μκ° λ³΅μ‘λκ° κ°λ€

- AVL : κ· νμ κ³μ μ‘λ BST





























































