# ✏Mark Down 작성법
(_2021-08-04~_)

## Text 입력 
`텍스트 입력은 그냥 이렇게`

## 1) 제목
```
#
##
###
####
#####
######

-> #이 많을수록 작아지는 제목!
```
💨
# T1
## T2
### T3
#### T4
##### T5
###### T6
</br>

❕ 또 다른 방법 
```
h1  or  h2
==      --    
```
💨 </br>

H1
==
H2
-- 
</br>

## 2) 코드블럭안에 source 넣기
1) enter </br>
    tab `source` </br>
    enter

   💨

            이것은 source입니다.


2)  백커터 3개를 사용합시다 </br>
    ` ``` ` </br>
        ` source ` </br>
    ` ``` `</br>

    💨
    ```
        이것도 source 입니다.
    ```
3) 백커터가 1개라면? </br> 
💨 `인라인 코드랍니다.`

4) 문법이 있는 언어를 코드블럭에 넣고 싶을 땐? </br>
` ```C ` </br>
`source` </br>
` ``` ` </br>

    💨</br>
    ```C
    #include <stdio.h>
    int main(void){
        printf("hello world");
    }
    ```

___
</br>

## 3) BlockQuote 사용하기
```
> text1
>> text2
>>> text3
```
💨 </br>
> text1
>> text2
>>> text3

___
</br>

## 4) 숫자 목록 
```
1.띄어쓰기 + text
2.띄어쓰기 + text
```
💨 </br>
1. text
2. text 

___
</br>

## 5) 순서 없는 목록 (글머리 기호)
```
+ t1 
    * t2
        - t3

+, *, - 간 순서는 상관 X
```
💨</br>
+ t1
    * t2
        - t3

___
</br>

## 6) 구분선 만들기 
```
--- (<- 헤더로 인식할 수 있으니 조심하기)
***
___

```

💨</br>

---
***
___

</br>

____

</br>

## 7) 문단 간격
문단 간격은 `</br>` 로 조절합니다.

___
</br>

## 8) 폰트 스타일 
```
__굵게__
**굵게**
_기울여쓰기_
*기울여쓰기*
~~취소선~~

```
💨</br>
__굵게__

**굵게**

_기울여쓰기_

*기울여쓰기*

~~취소선~~

___
</br>

## 9) 링크
1. 인라인 링크 
    ```
    [인라인 링크](https://lorlorv.tistory.com/)
    ```
2. url 링크
    ```
    <https://lorlorv.tistory.com/>
    ```
3. 참조 링크
    ```
    [tistory] : (https://lorlorv.tistory.com/)
    ```

💨 </br>

[인라인 링크](https://lorlorv.tistory.com/) </br>
 <https://lorlorv.tistory.com/> </br>
 [tistory] : (https://lorlorv.tistory.com/)

 ___
 </br>

 ## 10) 이미지 링크 
 ```
 ![이미지 설명] (이미지 링크)

 +) 이미지는 이 마크다운이 있는 폴더 안에 image폴더를 만들어 그 안에 저장한다음 가져오는 것이 편하다!
 ```
 💨 ![고양이](/Images/developer.jpeg)

 ```
 ❕이미지에 링크를 걸고싶다면?
[![이미지 설명](이미지 링크)](연결할 url " 마우스를 갖다대면 나타낼 text")
```
💨 [![고양고양](/Images/developer.jpeg)](https://lorlorv.tistory.com/ "야옹")

```
❕이미지는 gif도 가능
❕사이즈 조절 : html을 통한 이미지 업로드 후 
<img width = "" height = ""></img>
```
</br>
___

</br>

## 11) 테이블
테이블은 `|`로 구분합니다. </br>
* `|:` : 왼쪽 정렬 </br>
* `|: :|` : 양쪽 정렬</br>
* `:|` : 오른쪽 정렬</br>

```
| 날짜 | 종목 | 시간 |
|:---- |:----:|----:|
|8/2(월) | 야구(대한민국 : 이스라엘) | 오후 7:00 |
|8/3(화) | ~~축구(대한민국 : 멕시코)~~ | 오후 8:00|
|8/4(수) | **배구(대한민국 : 터키)** | 오전 9:00|
```

💨

| 날짜 | 종목 | 시간 |
|:---- |:----:|----:|
|8/2(월) | 야구(대한민국 : 이스라엘) | 오후 7:00 |
|8/3(화) | ~~축구(대한민국 : 멕시코)~~ | 오후 8:00|
|8/4(수) | **배구(대한민국 : 터키)** | 오전 9:00|

</br>

___
</br>

## 12) 체크박스 
```
-, *, + [띄어쓰기] <-비어있는 체크박스 
        [x] <- 체크된 체크박스 
```
💨</br>

* [ ] 공부하기
* [x] 운동하기

</br>

___
</br>

## 13) 글자 색상
```
<span style = "color : blue"> BLUE </span>
<span style = "color : #f58787">#f58787</span>
<span style = "color : rgb(135, 250, 35)"> BLUE </span>
```
💨</br>

<span style = "color : blue"> BLUE </span> </br>
<span style = "color : #f58787">#f587873</span> </br>
<span style = "color : rgb(135, 250, 35)">GREEN</span>
___
</br>

## 14) 같은 파일 내 위치 이동
```
[보여질 text 내용](#이동할-text-내용)


1. 띄어쓰기는 -(하이픈)
2. 영어는 모두 소문자!
```
[맨 처음으로!](#text-입력)

---
</br>

## 15) 접기/펼치기
```
<details markdown="1"> 
//markdown에는 기능이 없기 때문에 html의 details를 사용한다.
//markdown="1"의 의미 : 접기/펼치기 블록안에서 markdown의 문법을 사용한다!
<summary>접은 글의 제목</summary>

접은 글의 내용

</details>
```

<details markdown="1">
<summary>접은 글의 제목</summary>
접은 글의 내용
</details>
