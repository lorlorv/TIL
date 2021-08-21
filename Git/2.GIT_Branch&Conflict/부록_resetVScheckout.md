# 부록 : reset vs checkout
[checkout](#1.1-head-branch-commit-&-checkout)

## 1.1 Head Branch commit & checkout
## **`checkout == HEAD 제어!!`**

1. </br> 

    ![](/Images/gitImage/부록1.JPG)
    
    - ### `HEAD를 보고 알 수 있는 것`
        1. 현재 나의 저장소는 master branch에 checkout 되어있구나!
        2. 현재 나의 저장소는 master branch 상태구나!

    - ### `현재 이 저장소가 어떤 version으로 되어있는지 or 어떤 version 상태에 있는 지 알고싶다면?`
        → HEAD가 가리키는 MASTER가 가리키고 있는 이 version을 통해 알 수 있다.

2. </br> 

    ![](/Images/gitImage/부록2.JPG)

    - ### 현재 이 저장소의 version이 무엇인지는 HEAD를 따라가보면 알 수 있다. (==ver.2)
        → 새로운 branch의 시작 version도 알 수 있다.

 3. </br> 

    ![](/Images/gitImage/부록3.JPG)

    - ### HEAD를 보고 이 저장소가 **어떤 branch에 checkout**되어있는지, **이 저장소의 최신 상태**가 무엇인지 알 수 있다.

4. </br> 

    ![](/Images/gitImage/부록4.JPG)

    1. HEAD → Master 
    2. ver.2로 저장소를 바꾼다

    - ### **∴ checkout == HEAD의 값을 바꾸는 것!**

5. </br> 

    ![](/Images/gitImage/부록5.JPG)

    1. 1번 이라는 이름의 버전을 직접 가리킨다.
    2. 이 저장소는 1번 저장소의 상태가 된다.

    - ### ∴ HEAD가 branch를 가리키지 않고 커밋을 가리키는 상태
         → **"detached" 상태에 있다!** (branch와 떨어져 있다.)

## **`checkout == HEAD 제어!!`**
</br>

---
## 1.2 Reset

### `