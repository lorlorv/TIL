# 2. Git CLI - Branch & Conflict 🌳
[Branch](#branch)</br>
[Conflict](#conflict)


## Branch
지금까지 만들던 버전에 이어서 서로 다른 여러 작업을 진행해야할 때 
</br>-> 저장소를 복제하지 않고 동일한 효과를 낼 수 있는 방법!
### => **브랜치(branch)**

ex)</br>
나는 어떤 회사의 상품 사용 설명서를 작성하는 업무를 맡았다.</br>
상품이 출시되기 전, 고객사가 없을 때 사용 설명서는 
- [master] A->B->C->D ... 

이렇게 쉽게 순차적으로 버전관리를 이어나가면 된다.</br>
**하지만,** 고객사가 많이 생겼다면?  </br>
고객사마다 요구 사항이 다를 것이고 </br>
**그렇다면,** 고객사마다 맞춤 사용 설명서를 작성해야한다.

- [master]  : *A->B->C->D*
- [Apple]   : *A->B->C->D*->AE
- [Google]  : *A->B->C->D*->GE->GF
- [MS]      : *A->B->C->D*->ME

이렇게 *A->B->C->D*의 디렉토리가 공통됨 
### **->비효율적!**
</br>

### ❗ 문제점 
1. `버전 관리의 이유` :  파일 이름을 더럽히지 않고 버전을 관리하는 것.
    - **but** 고객사마다 디렉토리가 만들어져 디렉토리의 이름을 더럽히고 있다!
2. 다른 고객사에 있는 최신 버전을 가져올 때 그 전의 버전들은 복제되지 않는다.

### **브랜치를 사용하면 이런 문제점을 해결할 수 있다!**
Branch : 한 뿌리에서 나왔지만 서로 다른 역사를 써가고 있는 버전들

</br>

---

## Conflict
branch와 branch를 병합할 때  </br>
 ![conflict ex](/Images/conflict.JPG)

1. 서로 다른 파일을 병합할 때 
2. 같은 파일의 다른 부분을 수정하고 병합했을 때 
3. **같은 파일의 같은 부분을 수정했을 때?**
    - 이때 충돌(=conflict)이 일어난다.

## ✏ex) </br>
: o2 branch의 work.txt와 master branch의 work.txt의 같은 부분을 수정 후 병합 명령어를 입력했을 때 </br>
: "o2" branch의 내용을 → master branch로 합치기 
1. `git merge o2` : CONFLICT가 일어난 후 자동적으로 병합하는 것을 실패했으니 알아서 충돌을 해결하고 그 결과를 commit 하라는 error 메세지 등장 </br> 

    ![](/Images/gitImage/conflict.JPG)

- work.txt 파일 : </br>

    ![](/Images/gitImage/conflict_nano.JPG)
    - `=====` : 파일과 파일의 구분자 
2.  FIX : master, o2로 내용을 고쳐 conflict를 수정한다.</br>

    ![](/Images/gitImage/conflict해결.JPG)

3.  Fix 후 git commit 
    - → 자동으로 git merge
    - `git merge` 시 내용 : 충돌이 있었고 어떻게 해결했는지까지 message로 알 수 있다.
        
4. 해결 후 log : </br>

    ![](/Images/gitImage/conflict_log.JPG)

___
</br>

## Conflict 3 Way Merge
: git이 충돌을 처리하는 방법 
- ### `conflict` : 협업때도 일어남 (←branch를 사용하는 것이기 때문!)

![](/Images/gitImage/3-way-merge.JPG)



































