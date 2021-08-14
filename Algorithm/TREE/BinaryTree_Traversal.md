# 🛸이진트리의 순회 
`순회 (traversal)` </br> : 트리에 속하는 모든 노드들을 한번씩 방문하여 노드가 가지고 있는 데이터를 목적에 맞게 처리하는 것 

## 순회 방법 
1. 전위 순회(preorder treversal) : VLR
    - 자손 노드보다 루트 노드를 먼저 방문한다.
2. 중위 순회(inorder traversal) : LVR
    - 왼쪽 자손, 루트, 오른쪽 자손 순으로 방문한다.
3. 후위 순위(postorder traversal) : LRV
    - 루트 노드보다 자손을 먼저 방문한다.

### `전위 순회`
루트->왼쪽 서브 트리->오른쪽 서브 트리
- 순환호출 이용 
    ```C
    preorder(x):
        if x ≠ NULL
            then print DATA(X);
            preorder(LEFT(x));
            preorder(RIGHT(x));
    ```
- ex) 구조화 된 문서 출력 </br>

    ![](/Images/preorder.JPG)

### `중위 순회`
왼쪽 서브 트리->루트->오른쪽 서브 트리
- 순환호출 이용 
    ```C
    inorder(x):
        if x ≠ NULL
            then print DATA(X);
            inorder(LEFT(x));
            inorder(RIGHT(x));
    ```
- ex) 수식 트리 
    - [코드로 보는 수식 트리👀](#🎲수식트리) </br>

        ![](/Images/inorder.JPG)
 

### `후위 순회`
왼쪽 서브 트리->오른쪽 서브 트리->루트
- 순환호출 이용 
    ```C
    postorder(x):
        if x ≠ NULL
            then print DATA(X);
            postorder(LEFT(x));
            postorder(RIGHT(x));
    ```
- ex) 디렉토리 용량 계산

---
</br>

## ✍🏻반복적 순회
: 스택에 자식노드들을 저장하고 꺼내면서 순회한다.  </br>

![](/Images/반복적순회.JPG)


## ✍🏻레벨 순회
: 각 노드를 레벨 순으로 검사하는 순회 방법
- 알고리즘 
    ```C
    level_order(root):
        initialize queue;
        if(root == NULL)
            then return;
        enqueue(queue, root);
        while is_empty(queue) ≠ TRUE do
            x ← dequeue(queue);
            print x→data;
            if(x→left != NULL) then
                enqueue(queue, x→left);
            if(x→right != NULL) then
                enqueue(queue, x→right);
    ```
- 💻 레벨 순회 skeleton
    ```C
    //레벨 순회
    #include <stdio.h>
    #include <stdlib.h>
    #define MAX 100

    typedef struct TreeNode {
        int data;
        struct TreeNode* left, * right;
    }TreeNode;

    typedef TreeNode* element;
    typedef struct {
        element data[MAX];
        int front, rear;
    }QueueType;
    /*QUEUE 구현 함수들 */
    void level_order(TreeNode* t) {
        QueueType q;

        init_queue(&q);

        if (t == NULL)
            return;
        enqueue(&q, t);
        while (!is_empty(&q)) {
            t = dequeue(&q);
            printf("[%d] ", t->data);

            if (t->left != NULL)
                enqueue(&q,t->left);
            if (t->right != NULL)
                enqueue(&q, t->right);
        }
    }

    //      15
    //   4      20
    // 1       16 25

    TreeNode n1 = { 1, NULL, NULL };
    TreeNode n2 = { 4, &n1, NULL };
    TreeNode n3 = { 16, NULL, NULL };
    TreeNode n4 = { 25, NULL, NULL };
    TreeNode n5 = { 20, &n3, &n4 };
    TreeNode n6 = { 15, &n2, &n5 };
    TreeNode* root = &n6;

    int main(void) {
        printf("레벨 순회=");
        level_order(root);
        return 0;
    }
    ```

-  ### `pre/in/post 순회`
    - 재귀적
    - 반복적(스택을 명시적으로 사용)
- ### `level 순회`
    - 반복적(큐를 명시적으로 사용)

---
</br>

## 🎲수식트리
: 산술식을 트리 형태로 표현한 것 

- `비단말노드` : 연산자 (operator)
- `단말노드` : 피연산자(operand)

### `수식트리 계산 `
- 후위 순위를 사용
- 서브 트리의 값을 순환 호출로 계산
- 비단말 노드를 방문할 때 양쪽 서브트리의 값을 노드에 저장된 연산자를 이용하여 계산한다.

### `알고리즘`

```C
evaluate (exp)
    if exp = NULL
        then return 0;
    else
        x ← evaluate ( exp → left );
        y ← evaluate ( exp → right );
        op ← exp → data;  

    return (x op y);
```
1. 만약 수식트리가 공백이면
2. 그냥 복귀한다.
3. 그렇지 않으면 왼쪽 서브 트리를 계산하기 위해 evaluate를 다시 순환호출한다. 이때, 매개변수는 왼쪽 자식 노드가 된다.
4. 똑같은 식으로 오른쪽 서브 트리를 계산한다.
5. 추출된 연산자를 가지고 연산을 수행해서 반환한다.

</br>

- 💻수식트리 skeleton
    ```C
    //수식 계산 트리
    #include <stdio.h>

    typedef struct TreeNode {
        int data;
        struct TreeNode* left, * right;
    }TreeNode;

    int evaluate(TreeNode* t) {
        if (t == NULL)return 0;
        if (t->left == NULL && t->right == NULL) return t->data; //단말노드
        else {
            int op1 = evaluate(t->left); //왼쪽 서브 트리 계산
            int op2 = evaluate(t->right); //오른쪽 서브 트리 계산

            printf("%d %c %d을 계산합니다.\n", op1, t->data, op2);

            switch (t->data) {
            case '+':
                return op1 + op2;
            case '-':
                return op1 - op2;
            case '*':
                return op1 * op2;
            case '/':
                return op1 / op2;
            }
        }
        return 0;
    }
    //        +  
    //    *       /
    //  3  4     8  2

    TreeNode n1 = { 3, NULL, NULL };
    TreeNode n2 = { 4, NULL, NULL };
    TreeNode n3 = { '*', &n1, &n2 };
    TreeNode n4 = { 8, NULL, NULL };
    TreeNode n5 = { 2, NULL, NULL };
    TreeNode n6 = { '/', &n4, &n5 };
    TreeNode n7 = { '+', &n3, &n6 };
    TreeNode* root = &n7;

    int main(void) {
        printf("값은=%d\n", evaluate(root));
        return 0;
    }
    ```



