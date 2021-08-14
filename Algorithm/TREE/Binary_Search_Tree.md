# 🥑Binary Search Tree
## 이진 탐색 트리 
: 탐색작업을 효율적으로 하기 위한 자료구조 

## 정의
1. 모든 원소의 키는 유일한 키를 가진다.
2. 왼쪽 서브트리 키들은 루트의 키보다 작다.
3. 오른쪽 서브 트리의 키들은 루트의 키보다 크다.
4. 왼쪽과 오른쪽 서브트리도 이진 탐색 트리이다.

**: 이진 탐색을 중위 순회하면 오름차순으로 정렬된 값을 얻을 수 있다.**

---
</br>

## 탐색 구현
- 반복적 방법
- 순환적 방법

### `순환적인 탐색 연산`
: 루트 노드의 키 값과 주어진 탐색 키 값을 비교한 결과가
1. 같으면 탐색이 성공적으로 끝난다.
2. 주어진 키 값이 루트노드의 키 값보다 작으면 탐색은 이 루트 노드의 왼쪽 자식을 기준으로 다시 시작한다.
3. 주어진 키 값이 루트노드의 키 값보다 크면 탐색은 이 루트 노드의 오른쪽 자식을 기준으로 다시 시작한다.

### `순환적 알고리즘`
```C
Treenode *search (TreeNode *node, int key){
    if(node == NULL) return NULL;
    if(node → key == key) return node;
    else if(key < node → key)
        return search(node → left, key);
    else
        return search(node → right, key);
}
```

### `반복적 알고리즘`
```C
TreeNode *search (TreeNode *node, int key){
    while(node != NULL){
        if(key == node → key) return node;
        else if(key < node → key)
            node = node → left;
        else
            node = node → right;
    }
    return NULL;
}
```
## 삽입 연산
: 먼저 탐색 수행 필요! </br>
### **`이유`** 
1. 같은 키 값을 갖는 노드 없어야 함
2. 탐색에 실패한 위치가 삽입하는 위치!

    ![](/Images/insert_bst.JPG)

### **`알고리즘`**
```C
TreeNode *insert(TreeNode *node, int key){
    if(node == NULL) return NULL;
    if(key < node → key )
        node → left = insert(node → left, key);
    else if(key > node → key)
        node → right = insert(node → right, key);
    
    return node;
}
```
## 삭제 연산
: 고려사항
1. 삭제하려는 노드가 단말노드일 경우
2. 삭제하려는 노드가 하나의 왼쪽이나 오른쪽 서브트리만을 가지고 있는 경우
3. 삭제하려는 노드가 두개의 서브트리 모두 가지고 있는 경우

![](/Images/delete_3case.JPG)
- case 1
    - 단말노드 삭제, 부모노드 링크 NULL
- case 2
    - 노드 삭제, 서브 트리는 부모노드에 붙이기
- case 3
    - 삭제노드와 가장 비슷한 값 노드를 삭제 노드 위치로
        - **가장 비슷한 값 노드는 어디에 있을까?** </br>
            1. 왼쪽 서브트리에서 가장 큰 값
            2. 오른쪽 서브 트리에서 가장 작은 값

### `알고리즘`
```C
    //case 1, 2 :
    if(root → left == NULL){
        TreeNode *temp = root → right;
        free(root);
        return temp;
    }

    else if(root → right == NULL){
        TreeNode *temp = root → left;
        free(root);
        return temp;
    }
    //case 3:
    TreeNode *temp = min_value_node(root → right);
    root → key = temp → key;
    root → right = delete_node(root → right, temp → key);

```

