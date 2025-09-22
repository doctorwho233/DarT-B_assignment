# SQL_BASIC 3주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_3rd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**3주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **7 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 3문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_3rd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-6. 연습문제 1~3번

### 2-6. 연습문제 7~9번

### 2-6. 연습문제 10~12번

### 2-6. 연습문제 13~17번

### 2-7. 정리 

### 2-8. 새로운 집계함수



## 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-1. INTRO

### 3-2. SQL 쿼리 작성하는 흐름

### 3-3. 쿼리 작성 템플릿과 생산성 도구 



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 2-6. 연습문제

~~~
✅ 학습 목표 :
* 연습문제(7문제 이상) 푼 것들 정리하기
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
### 문제 1  
![alt text](image-4.png)

~~~ sql
SELECT
  COUNT(id) AS cnt
FROM basic.poketmon
WHERE
  (type2 IS NULL)
~~~
### 문제 2
![alt text](image-5.png)
~~~ sql
SELECT
  type1,
    COUNT(id) AS pokemon_cnt
FROM
  basic.poketmon
WHERE
  type2 IS NULL
GROUP BY
  type1
ORDER BY
  pokemon_cnt DESC
  ~~~
### 문제 3
![alt text](image-6.png)
~~~ sql
SELECT
    type1,
        COUNT(id) AS pokemon_cnt
FROM
    basic.poketmon
GrOUP BY
    type1
~~~
### 문제 4
![alt text](image-7.png)
~~~ sql
SELECT
    is_legendary,
        COUNT(id) AS pokemon_cnt
FrOM
    basic.poketmon
GROUP BY
    is_legendary
~~~
### 문제 5
![alt text](image-8.png)
~~~ sql
SELECT
    name,
    COUNT(name) AS cnt
FROM
    basic.poketmon
group by
    name
HAVING
    cnt > 1
~~~
### 문제 6
![alt text](image-9.png)
~~~ sql
SELECT
    *
FROM
    basic.trainer
WHERE
    name = 'iris'
~~~
### 문제 7
![alt text](image-10.png)

~~~ sql
SELECT
    *
FROM
    basic.trainer
WHERE
    name = 'iris'
    OR name = 'Whitney'
    OR name = 'Cynthia'
~~~



✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE을 활용하는 방법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/02975c80-b8d9-4ca1-9938-62cff6704224" />
조건(필터링) - WHERE : 어떤 조건으로 볼까? <br>
추출 - SELECT : 뭐 볼까? <br>
FROM : 어디서 볼까? <br>
요약 - GROUP BY : 어떻게 나눠서 볼까? <br>


## 3-2. 쿼리를 작성하는 흐름

~~~
✅ 학습 목표 :
* 쿼리를 작성하는 흐름을 설명할 수 있다.
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
지표고민 - 목적 <br>
지표 구체화 - 정의 <br>
지표 탐색 - 히스토리 <br>
쿼리 작성 - 히스토리 없을 때 -1개(활용)<br>
                            -2개(연결방법 JOIN)<br>
데이터 정합성 확인 - 결과확인<br>
쿼리 가독성 - 나중을 위해서<br>
쿼리 저장 - 문서로 저장


## 3-3. 쿼리 작성 템플릿과 생산성 도구

~~~
✅ 학습 목표 :
* 생산성 도구를 만들 수 있다.
~~~

<!-- 이어질 주차에서 생산성 도구를 활용한 실습이 있습니다.강의에 맞게 제작하여 화면을 캡쳐하여 이 주석을 지우고 올려주세요. -->
이 부분은 문제가 있어서 우선은 안해도 된다고 하셔서 따로 정리는 하지 않았습니다.


<br>
<br>

---

# 2️⃣ 학습 인증란

<<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8b17aab5-287e-468d-9486-bdd7e5c0bb0a" />
>


<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. 포켓몬 게임에 재미를 느낀 동혁은 포켓몬 도감에서 강력한 포켓몬 타입을 미리 선점하기 위해, 먼저 어떤 포켓몬들이 있는지 포켓몬 수를 기준으로 내림차순 정렬하여  확인하고자 했습니다.**
>
> 그래서 다음과 같은 필요한 정보를 미리 정리해보았습니다. 

~~~
조건 : type2는 상관없이
보고 싶은 컬럼 : type1
집계 내용 : 각 type1 별 포켓몬 수
정렬 기준 : 포켓몬 수를 기준으로 내림차순 정렬
~~~

> **이 목표를 바탕으로 동혁이 아래와 같은 쿼리를 잘 작성했지만, 일부 SQL 문법 요소를 빼먹었습니다. 비어 있는 부분인 ㄱ,ㄴ,ㄷ 에 들어갈 알맞은 SQL 구문을 채워보세요:**

~~~sql
SELECT type1, (ㄱ)
FROM pokemon
(ㄴ) type1
ORDER BY (ㄱ) (ㄷ);
~~~



~~~
SELECT type1, COUNT(*)
FROM pokemon
GROUP BY type1
ORDER BY COUNT(*) DESC;

ㄱ : COUNT(*)

ㄴ : GROUP BY

ㄷ : DESC
~~~



### 🎉 수고하셨습니다.
