# SQL_BASIC 2주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_2nd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**2주차 과제**는 1주차 과제처럼 SQL의 필요성이나 느낀점 위주가 아닌, **실제 강의 내용을 바탕으로 개념을 정리하고 학습한 내용을 집중적으로 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요. 

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_2nd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

### 2-4. SELECT 연습문제

### 2-5. 집계 (Group By + Having + Sum/Count)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | 🍽️         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리 

## 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE의 핵심 문법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
**SELECT** <br>
기본 문법 <br><br>
SELECT : 어떤 컬럼 선택할지 <br>
  Col1 AS new_name, (따옴표 없이 실행) <br>
  Col2, <br>
  Col3 <br>
FROM Dataset.Table : 어떤 테이블에서 데이터 확인할지(프로젝트 id/dataset/table) <br>
WHERE : 조건 <br>
  Col1 = 1 : 조건문 <br><br>

* EXCEPT(제외할 컬럼) <br>
테이블 간 교집합 부분은 JOIN 활용 <br>

<img width="844" height="366" alt="image" src="https://github.com/user-attachments/assets/15aa579f-4c0a-4072-92fb-d4c357e8ffe3" />


## 2-5. 집계 (Group By / HAVING / SUM,COUNT)

~~~
✅ 학습 목표 :
* 데이터를 집계하고 그룹화하는 방법을 설명할 수 있다.
* GROUP BY, HAVING, ORDER BY, 집계함수(SUM/COUNT 등)을 활용하는 방법을 설명할 수 있다.
* having과 where의 차이에 대해서 설명할 수 있다.
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
GROUP BY : 같은 값끼리 모아서 그룹화 -**특정 컬럼 기준으로 모으면서 다른 컬럼에선 집계 가능**  <br>
'평균' '개수' 자주 사용 <br>
SELECT <br>
  집계할 컬럼 1,<br>
  집계 함수(COUNT,MAX,MIN 등)<br>
FROM Table<br>
Group BY<br>
  집계할 컬럼<br>
DISTINT : 중복제거<br>
<img width="839" height="444" alt="image" src="https://github.com/user-attachments/assets/71378011-f03e-4bb9-bfb1-1e0dfcbb9d0f" /> <br>
WHERE : Table에 바로 조건을 설정하고 싶은 경우<br>
HAVING : GROUP BY 한 후 조건을 설정하고 싶은 경우 사용<br>
서브쿼리 : SELECT 문 안에 존재하는 SELECT 쿼리<br>
ORDER BY : 정렬 순서 DESC(내림차순) QSC(오름차순 -보통 디폴트)<br>
  쿼리 맨 마지막에 두고 중간에 둘 필요 없음<br>
LIMIT : 쿼리문의 결과 ROW 수를 제한하고 싶은 경우 쿼리문의 제일 마지막에 작성 <br>
Ex) <br>
ORDER BY ()<br>
LIMIT 10



# 2️⃣ 학습 인증란

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ee3111d9-67b1-487b-a2f9-51955c2b38bd" />




<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. 포켓몬 마스터 승화는 포켓몬 데이터 조회하는 SQL문에 재미를 느껴서 혼자서 데이터를 조회하는 쿼리문을 짰습니다. 하지만 세 가지의 오류로 다음 코드가 실행이 안된다고 하는데, 각 오류의 위치와 이유를 설명하고, 올바른 쿼리문으로 수정해보세요.**

~~~sql
# 승화의 SQL Query문 
SELECT name AS '포켓몬 이름', ID;
WHERE type = 'Electric';
FROM pokemon;
~~~



~~~
1. 세미콜론 때문에 문장이 끝나 각 문장이 이어지지 않아 오류가 남
2. SELECT -> FROM -> WHERE 의 순서가 되어야 함
3. 이름 지정에 따옴표가 있으면 안된다.

SELECT name AS 포켓몬 이름, ID 
FROM pokemon 
WHERE type = Electric; 


~~~



## 문제 2

> **🧚Q. 앞서 SQL Query의 오류를 해결한 승화는 기분 좋게 이번에는 포켓몬 데이터에서 타입별 평균 공격력이 60 이상인 타입만 조회하려는 쿼리를 작성하려고 했습니다. 하지만 이번에도 실수를 하여 쿼리문이 실행되지 않거나 잘못된 결과가 나오고 있는데, 쿼리에서 잘못된 부분이 무엇인지 설명하고, 올바르게 수정한 쿼리를 작성해보세요.**

~~~sql
SELECT type, AVG(attack) AS avg_attack 
FROM pokemon
WHERE AVG(attack) >= 60
GROUP BY type;
~~~



~~~
1. WHERE 안에서 집계함수를 사용함.(WHERE 이 아니라 HAVING 써야함) 
2. SELECT -> FROM -> GROUP BY -> HAVING 순이어야 함 

SELECT type, AVG(attack) AS avg_attack
FROM pokemon
GROUP BY type
HAVING AVG(attack) >= 60;
~~~



### 🎉 수고하셨습니다.
