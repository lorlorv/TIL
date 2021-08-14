# 🍒Binary Tree
## 이진트리 
: 모든 노드가 2개의 서브 트리를 가지고 있는 트리 </br>
`서브 트리는 공집합일 수 있다.`

1. 이진트리의 노드에는 최대 2개까지의 자식 노드가 존재한다.
2. 모든 노드의 차수가 2 이하가 된다.
    - 구현이 편리하다!
3. 이진트리에는 서브 트리간의 순서가 존재한다.

### ✏정의
```
1) 이진트리는 공집합이며
2) 루트와 왼쪽 서브트리, 오른쪽 서브트리로 구성된 노드들의 유한 집합으로 정의된다. 이진트리의 서브 트리들은 모두 이진 트리이어야한다.
```
---

### ✏성질
### `간선의 개수 `
- 노드의 개수가 n개일 때 간선의 개수는 **n-1**이다.
    - 모든 노드는 루트 노드를 제외하면 정확하게 하나의 부모노드를 가지기 때문!

### `높이가 h인 이진트리의 노드 개수`
- MAX : 2^h - 1
- MIN : h </br>

    ![h](/Images/height.JPG)

### `n개의 노드를 가지는 이진트리의 높이`
- MAX : n
- MIN : ┌log₂(n+1)​┐ </br>
---

### ✏분류
- 포화 이진 트리(full binary tree)
- 완전 이진 트리(complete binary tree)
- 기타 이진 트리 </br>

    ![분류](/Images/이진트리분류.JPG)

### `포화 이진 트리`
트리의 각 level에 노드가 꽉 차있는 이진 트리
- 2ⁿ - 1개의 노드를 갖는다. (높이 : n)
- 노드 번호 부여
    - 레벨 단위로 왼쪽에서 오른쪽 순서로 번호가 부여된다. </br>

### `완전 이진 트리`
level 1부터 k - 1까지는 모두 채워져 있고 마지막 level k에서는 왼쪽에서 오른쪽 순서대로 채워져있다.
- 완전 이진 트리의 잘못된 예)</br>

    ![완전이진x](/Images/완전이진x.JPG)

- 포화 이진 트리 -> 완전 이진 트리 ⭕
- 완전 이진 트리 -> 포화 이진 트리 ❌
---

### ✏이진트리의 표현 
- 배열
- 포인터

### `배열 표현법`
모든 이진 트리를 포화 이진트리라고 가정하고 각 노드에 번호를 붙여 그 번호를 배열의 인덱스로 삼아 노드의 데이터를 배열에 저장하는 방법
- 깊이가 k일 때, 최대 2^k - 1개의 공간을 연속적으로 할당한다.
    - ->이진트리의 번호대로 노드들을 배열에 저장한다. </br>
    `인덱스 0은 사용되지 않음!`
- 단점) 기억공간의 낭비가 크다. </br>

    ![배열표현법](/Images/배열표현법.JPG)


- `노드 i의 부모 노드 인덱스` : i / 2
- `노드 i의 왼쪽 자식 노드 인덱스` : 2i
- `노드 i의 오른쪽 자식 노드 인덱스` : 2i + 1

### `링크 표현법`
트리에서의 노드가 구조체로 표현, 각 노드가 포인터를 가지고 있어 이 포인터를 이용하여 노드와 노드를 연결한다. </br>

![linked](/Images/링크표현법.JPG) </br>

![linkedImage](/Images/링크표현법_그림.JPG)

- 링크의 구현 
    - 노드는 구조체로 표현
    - 링크는 포인터로 표현

        ```C
        typedef struct TreeNode{
            int data;
            struct TreeNode *left, *right;
        }TreeNode;
        ```

    - 💻링크표현법으로 생성된 이진트리 
        ```C
        //링크 표현법으로 생성된 이진트리 skeleton
        #include <stdio.h>

        typedef struct TreeNode {
            int data;
            struct TreeNode* left, * right;
        }TreeNode;
        //     n1
        //    /  |
        //   n2  n3
        int main(void) {
            TreeNode* n1, * n2, * n3;
            n1 = (TreeNode*)malloc(sizeof(TreeNode));
            n2 = (TreeNode*)malloc(sizeof(TreeNode));
            n3 = (TreeNode*)malloc(sizeof(TreeNode));

            n1->data = 10;
            n1->left = n2;
            n1->right = n3;

            n2->data = 20;
            n2->left = NULL;
            n2->right = NULL;

            n3->data = 30;
            n3->left = NULL;
            n3->right = NULL;

            free(n1); free(n2); free(n3);
            return 0;
        }
        ```
---
</br>

## 이진 트리의 추가 연산

- ### `노드의 개수`
    ```C
    int get_node_count(TreeNode *node){
        int count = 0;
        if(node != NULL)
        count = 1 + get_node_count(node→left) + get_node_count(node→right);
        return count;
    }
    ```

- ### `단말 노드의 개수`
    ```C
    int get_leaf_count(TreeNode *node){
        int count = 0;
        if(node != NULL){
            if(node→left == NULL && node→right == NULL)
                return 1;
            else
                count = get_leaf_count(node→left) + get_leaf_count(node→right);
        }
        return count;
    }
    ```

- ### `높이 구하기`
    ```C
    int get_height(TreeNode *node){
        int height = 0;
        if(node != NULL){
            height = 1 + MAX(get_height(node→left), get_height(node→right))
        }
    }






























