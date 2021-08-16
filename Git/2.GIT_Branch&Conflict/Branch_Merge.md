# GIT : MERGE
브랜치 병합
- [Conflict_3_Way_Merge](#conflict-3-way-merge)
- [외부 도구를 이용한 병합](#외부-도구를-이용한-병합)
## 정의
## `MERGE` : 병합한다.
![](/Images/gitImage/merge개념.JPG)

- a에서 작업했던 내용이 master에서도 유용할 것 같을 때 → **merge!** (합치는 작업)
- git은 merge를 자동으로 해주는 시스템이 있고, **자동화하는게 논리적으로 불가능한 작업은 선별하여 우리에게 수동으로 작업**하게 한다.

## 용어 
- ### `base`: 합치려고 하는 공통의 조상
    ![](/Images/gitImage/base.JPG)
- ### `merge commit` : 서로 다른 브랜치에 있는 버전들을 합쳐 commit 하는 것 
    ![](/Images/gitImage/mergeCommit.JPG)
## 명령어
- ### `git commit --amend : 나중에 commit message를 수정할 수 있는 commit 명령어 

## merge 방법
ex) "o2" branch의 내용을 → master branch로 합치기 
1. ### `git checkout master` : 합친 내용을 담을 branch로 HEAD를 변경
2. ### `git merge o2` : 이 명령어를 입력하면 이 merge가 왜 만들어지는 지에 대한 설명을 작성할 수 있는 편집기가 실행됨 
    - 
        ```
        "Merge branch 'o2'" ← merge 행위에 대한 설명 
        == "o2" branch를 merge하면서 생긴 merge commit 
    -  ![](/Images/gitImage/merge_commit.JPG)

### 💡파일명이 같은 파일을 병합하면 어떻게 되는가?
- if) **같은 파일명이더라도 다른 부분**을 수정했다면?
    - git이 알아서 merge를 해준다. </br>
        - #### (원래 운영체제가 가지고 있는 기능 'copy'로는 안되는 기능/ git이라서 가능한 것!)
    
- if) **같은 파일명의 같은 부분**을 수정했다면?
    - ### [*conflict!*](/Git/2.GIT_Branch&Conflict/GIT-Branch&Conflict.md)

---
</br>

## Conflict 3 Way Merge
: git이 충돌을 처리하는 방법 
- ### `conflict` : 협업때도 일어남 (←branch를 사용하는 것이기 때문!)

![](/Images/gitImage/3-way-merge.JPG)

---
</br>

## 외부 도구를 이용한 병합
### `git mergetool`

### 👉🏻세팅
1. 검색창 → p4Merge → download!
2. `git config --global merge.tool p4mergetool
    - ~/.gitconfig
        ```
        [merge]
            tool = p4mergetool
         ```
3. `git config --global mergetool.p4merge.path '경로'`    

### 👉🏻실행
4. `git mergetool`

- **LOCAL** : HERE 현재 속해있는 branch
- **REMOTE** : THERE 땡겨올 branch

### 👉🏻작업 후 
→ 자동으로 add까지 해준다.

- `work.txt.org` : 이전 상태를 백업해놓음
- `work.txt` : 바꾼 내용 

- 바꾼 내용이 확실하다면 .org 지우기 
    - `rm ~`

___
출처 : [생활코딩](https://opentutorials.org/course/3839)

