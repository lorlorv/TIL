# ๐ธ์ด์งํธ๋ฆฌ์ ์ํ 
`์ํ (traversal)` </br> : ํธ๋ฆฌ์ ์ํ๋ ๋ชจ๋  ๋ธ๋๋ค์ ํ๋ฒ์ฉ ๋ฐฉ๋ฌธํ์ฌ ๋ธ๋๊ฐ ๊ฐ์ง๊ณ  ์๋ ๋ฐ์ดํฐ๋ฅผ ๋ชฉ์ ์ ๋ง๊ฒ ์ฒ๋ฆฌํ๋ ๊ฒ 

## ์ํ ๋ฐฉ๋ฒ 
1. ์ ์ ์ํ(preorder treversal) : VLR
    - ์์ ๋ธ๋๋ณด๋ค ๋ฃจํธ ๋ธ๋๋ฅผ ๋จผ์  ๋ฐฉ๋ฌธํ๋ค.
2. ์ค์ ์ํ(inorder traversal) : LVR
    - ์ผ์ชฝ ์์, ๋ฃจํธ, ์ค๋ฅธ์ชฝ ์์ ์์ผ๋ก ๋ฐฉ๋ฌธํ๋ค.
3. ํ์ ์์(postorder traversal) : LRV
    - ๋ฃจํธ ๋ธ๋๋ณด๋ค ์์์ ๋จผ์  ๋ฐฉ๋ฌธํ๋ค.

### `์ ์ ์ํ`
๋ฃจํธ->์ผ์ชฝ ์๋ธ ํธ๋ฆฌ->์ค๋ฅธ์ชฝ ์๋ธ ํธ๋ฆฌ
- ์ํํธ์ถ ์ด์ฉ 
    ```C
    preorder(x):
        if x โ  NULL
            then print DATA(X);
            preorder(LEFT(x));
            preorder(RIGHT(x));
    ```
- ex) ๊ตฌ์กฐํ ๋ ๋ฌธ์ ์ถ๋ ฅ </br>

    ![](/Images/preorder.JPG)

### `์ค์ ์ํ`
์ผ์ชฝ ์๋ธ ํธ๋ฆฌ->๋ฃจํธ->์ค๋ฅธ์ชฝ ์๋ธ ํธ๋ฆฌ
- ์ํํธ์ถ ์ด์ฉ 
    ```C
    inorder(x):
        if x โ  NULL
            then print DATA(X);
            inorder(LEFT(x));
            inorder(RIGHT(x));
    ```
- ex) ์์ ํธ๋ฆฌ 
    - [์ฝ๋๋ก ๋ณด๋ ์์ ํธ๋ฆฌ๐](#๐ฒ์์ํธ๋ฆฌ) </br>

        ![](/Images/inorder.JPG)
 

### `ํ์ ์ํ`
์ผ์ชฝ ์๋ธ ํธ๋ฆฌ->์ค๋ฅธ์ชฝ ์๋ธ ํธ๋ฆฌ->๋ฃจํธ
- ์ํํธ์ถ ์ด์ฉ 
    ```C
    postorder(x):
        if x โ  NULL
            then print DATA(X);
            postorder(LEFT(x));
            postorder(RIGHT(x));
    ```
- ex) ๋๋ ํ ๋ฆฌ ์ฉ๋ ๊ณ์ฐ

---
</br>

## โ๐ป๋ฐ๋ณต์  ์ํ
: ์คํ์ ์์๋ธ๋๋ค์ ์ ์ฅํ๊ณ  ๊บผ๋ด๋ฉด์ ์ํํ๋ค.  </br>

![](/Images/๋ฐ๋ณต์ ์ํ.JPG)


## โ๐ป๋ ๋ฒจ ์ํ
: ๊ฐ ๋ธ๋๋ฅผ ๋ ๋ฒจ ์์ผ๋ก ๊ฒ์ฌํ๋ ์ํ ๋ฐฉ๋ฒ
- ์๊ณ ๋ฆฌ์ฆ 
    ```C
    level_order(root):
        initialize queue;
        if(root == NULL)
            then return;
        enqueue(queue, root);
        while is_empty(queue) โ  TRUE do
            x โ dequeue(queue);
            print xโdata;
            if(xโleft != NULL) then
                enqueue(queue, xโleft);
            if(xโright != NULL) then
                enqueue(queue, xโright);
    ```
- ๐ป ๋ ๋ฒจ ์ํ skeleton
    ```C
    //๋ ๋ฒจ ์ํ
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
    /*QUEUE ๊ตฌํ ํจ์๋ค */
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
        printf("๋ ๋ฒจ ์ํ=");
        level_order(root);
        return 0;
    }
    ```

-  ### `pre/in/post ์ํ`
    - ์ฌ๊ท์ 
    - ๋ฐ๋ณต์ (์คํ์ ๋ช์์ ์ผ๋ก ์ฌ์ฉ)
- ### `level ์ํ`
    - ๋ฐ๋ณต์ (ํ๋ฅผ ๋ช์์ ์ผ๋ก ์ฌ์ฉ)

---
</br>

## ๐ฒ์์ํธ๋ฆฌ
: ์ฐ์ ์์ ํธ๋ฆฌ ํํ๋ก ํํํ ๊ฒ 

- `๋น๋จ๋ง๋ธ๋` : ์ฐ์ฐ์ (operator)
- `๋จ๋ง๋ธ๋` : ํผ์ฐ์ฐ์(operand)

### `์์ํธ๋ฆฌ ๊ณ์ฐ `
- ํ์ ์์๋ฅผ ์ฌ์ฉ
- ์๋ธ ํธ๋ฆฌ์ ๊ฐ์ ์ํ ํธ์ถ๋ก ๊ณ์ฐ
- ๋น๋จ๋ง ๋ธ๋๋ฅผ ๋ฐฉ๋ฌธํ  ๋ ์์ชฝ ์๋ธํธ๋ฆฌ์ ๊ฐ์ ๋ธ๋์ ์ ์ฅ๋ ์ฐ์ฐ์๋ฅผ ์ด์ฉํ์ฌ ๊ณ์ฐํ๋ค.

### `์๊ณ ๋ฆฌ์ฆ`

```C
evaluate (exp)
    if exp = NULL
        then return 0;
    else
        x โ evaluate ( exp โ left );
        y โ evaluate ( exp โ right );
        op โ exp โ data;  

    return (x op y);
```
1. ๋ง์ฝ ์์ํธ๋ฆฌ๊ฐ ๊ณต๋ฐฑ์ด๋ฉด
2. ๊ทธ๋ฅ ๋ณต๊ทํ๋ค.
3. ๊ทธ๋ ์ง ์์ผ๋ฉด ์ผ์ชฝ ์๋ธ ํธ๋ฆฌ๋ฅผ ๊ณ์ฐํ๊ธฐ ์ํด evaluate๋ฅผ ๋ค์ ์ํํธ์ถํ๋ค. ์ด๋, ๋งค๊ฐ๋ณ์๋ ์ผ์ชฝ ์์ ๋ธ๋๊ฐ ๋๋ค.
4. ๋๊ฐ์ ์์ผ๋ก ์ค๋ฅธ์ชฝ ์๋ธ ํธ๋ฆฌ๋ฅผ ๊ณ์ฐํ๋ค.
5. ์ถ์ถ๋ ์ฐ์ฐ์๋ฅผ ๊ฐ์ง๊ณ  ์ฐ์ฐ์ ์ํํด์ ๋ฐํํ๋ค.

</br>

- ๐ป์์ํธ๋ฆฌ skeleton
    ```C
    //์์ ๊ณ์ฐ ํธ๋ฆฌ
    #include <stdio.h>

    typedef struct TreeNode {
        int data;
        struct TreeNode* left, * right;
    }TreeNode;

    int evaluate(TreeNode* t) {
        if (t == NULL)return 0;
        if (t->left == NULL && t->right == NULL) return t->data; //๋จ๋ง๋ธ๋
        else {
            int op1 = evaluate(t->left); //์ผ์ชฝ ์๋ธ ํธ๋ฆฌ ๊ณ์ฐ
            int op2 = evaluate(t->right); //์ค๋ฅธ์ชฝ ์๋ธ ํธ๋ฆฌ ๊ณ์ฐ

            printf("%d %c %d์ ๊ณ์ฐํฉ๋๋ค.\n", op1, t->data, op2);

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
        printf("๊ฐ์=%d\n", evaluate(root));
        return 0;
    }
    ```



