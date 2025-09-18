# SQL_ADVANCED 1주차 정규 과제 

## Week 1 : 서브쿼리 & CTE

📌**SQL_ADVANCED 정규과제**는 매주 정해진 주제에 따라 **MySQL 공식 문서 또는 한글 블로그 자료를 참고해 개념을 정리한 후, 프로그래머스 SQL 3문제**와 **추가 확인문제**를 직접 풀어보며 학습하는 과제입니다. 

이번 주는 아래의 **SQL_ADVANCED_0th_TIL**에 나열된 주제를 중심으로 개념을 학습하고, 주차별 **학습 목표**에 맞게 정리해주세요. 정리한 내용은 GitHub에 업로드한 후, **스프레드시트의 'SQL' 시트에 링크를 제출**해주세요. 



**👀 (수행 인증샷은 필수입니다.)** 

> 프로그래머스 문제를 풀고 '정답입니다' 문구를 캡쳐해서 올려주시면 됩니다. 



## SQL_ADVANCED_1st_TIL 

### 15.2.15. SubQueries

#### 특히 15.2.15.1 ~ 15.2.15.7 (Scalar, EXISTS, Correlated, Derived 등) 

### 15.2.20 WITH (Common Table Expressions)

- `WITH RECURSIVE`에 대한 내용은 추후에 공부합니다. 해당 링크에서 `WITH`에 해당하는 부분만 정리해보세요. 




## 🏁 주차별 학습 (Study Schedule)

| 주차  | 공부 범위               | 완료 여부 |
| ----- | ----------------------- | --------- |
| 1주차 | 서브쿼리 & CTE          | ✅         |
| 2주차 | 집합 연산자 & 그룹 함수 | 🍽️         |
| 3주차 | 윈도우 함수             | 🍽️         |
| 4주차 | Top N 쿼리              | 🍽️         |
| 5주차 | 계층형 질의와 셀프 조인 | 🍽️         |
| 6주차 | PIVOT / UNPIVOT         | 🍽️         |
| 7주차 | 정규 표현식             | 🍽️         |

<br>


### 공식 문서 활용 팁

>  **MySQL 공식 문서는 영어로 제공되지만, 크롬 브라우저에서 공식 문서를 열고 이 페이지 번역하기에서 한국어를 선택하면 번역된 버전으로 확인할 수 있습니다. 다만, 번역본은 문맥이 어색한 부분이 종종 있으니 영어 원문과 한국어 번역본을 왔다 갔다 하며 확인하거나, 교육팀장의 정리 예시를 참고하셔도 괜찮습니다.**



# 1️⃣ 학습 내용 

> 아래의 링크를 통해 *MySQL 공식문서*로 이동하실 수 있습니다.
>
> - SubQueries : MySQL 공식문서 
>
> https://dev.mysql.com/doc/refman/8.0/en/subqueries.html
>
> (한국어 버전)
> https://dart-b-official.github.io/posts/mysql-subqueries/


> - CTE(공통 테이블 표현식) : MySQL 공식문서
>
> https://dev.mysql.com/doc/refman/8.0/en/with.html
>
> (한국어 버전)
> https://dart-b-official.github.io/posts/mysql-cte/

<br>
<br>
<!-- 여기까진 그대로 둬 주세요-->





# 2️⃣ 학습 내용 정리하기

---

 # 1. 서브쿼리

~~~
✅ 학습 목표 :
* SubQueries에 대한 문법을 이해하고 활용할 수 있다.  
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
# MySQL 서브쿼리 정리

## 1. 서브쿼리란?
- 하나의 SQL 문 안에 포함된 또 다른 `SELECT` 문을 의미한다.  
- 외부 쿼리(outer query)의 일부로 사용되며, 항상 괄호로 감싸야 한다.  
- 중첩이 가능하며, 여러 단계로 쌓을 수 있다.

---

## 2. 서브쿼리의 장점
- 쿼리를 구조적으로 분리하여 가독성을 높일 수 있다.  
- 복잡한 `JOIN`이나 `UNION`을 대체할 수 있다.  
- 선언적으로 “무엇을 구할지”를 중심으로 작성할 수 있다.

---

## 3. 서브쿼리 결과 형태
- **Scalar**: 단일 값(한 행, 한 컬럼).  
- **Column**: 하나의 컬럼, 여러 행 가능.  
- **Row**: 하나의 행, 여러 컬럼.  
- **Table**: 여러 행과 여러 컬럼, 테이블처럼 사용.

---

## 4. 서브쿼리를 사용할 수 있는 위치
- `SELECT` 절  
- `WHERE` 절  
- `HAVING` 절  
- `INSERT`, `UPDATE`, `DELETE` 문의 조건절  
- `SET`, `DO` 구문 등 다양한 위치

---

## 5. 주요 유형
- **Scalar comparison**: 하나의 값과 비교 (`=`, `<`, `>` 등).  
- **ANY / SOME / IN**: 여러 값 중 하나라도 만족하면 참.  
- **ALL / NOT IN**: 여러 값 모두와 비교하여 만족해야 함.  
- **Row Subquery**: 여러 컬럼을 묶어서 행 단위로 비교.  
- **EXISTS / NOT EXISTS**: 서브쿼리 결과의 존재 여부 확인.

---

## 6. 상관 서브쿼리 (Correlated Subquery)
- 서브쿼리가 외부 쿼리의 컬럼을 참조하는 경우.  
- 외부 쿼리의 각 행마다 서브쿼리가 반복 실행된다.  
- 데이터 양이 많을 경우 성능이 저하될 수 있다.  
- MySQL 최신 버전에서는 파생 테이블과 `JOIN`으로 최적화되는 경우가 있다.

---

## 7. 주의사항
- **스칼라 서브쿼리**는 반드시 하나의 값만 반환해야 한다.  
- **NULL 처리**: `ANY`, `ALL`, `IN`, `NOT IN`에서 NULL이 포함되면 예상치 못한 결과가 발생할 수 있다.  
- **`NOT IN`과 `<> ALL`** 은 동일하게 해석된다.  
- **Row Subquery** 비교 시 컬럼 개수가 일치해야 한다.  


# 2. CTE

~~~
✅ 학습 목표 :
* CTE에 대한 문법을 이해하고 활용할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
# MySQL CTE (Common Table Expressions) 정리

## 1. CTE란?
- SQL 문 안에서만 존재하는 이름 있는 임시 결과 집합.  
- 복잡한 쿼리를 구조적으로 나눠 가독성과 관리성을 높인다.  
- `WITH` 절로 정의하며, 이후 쿼리에서 테이블처럼 참조 가능.

---

## 2. 특징
- 하나의 SQL 문에서만 유효하다.  
- 여러 번 참조 가능하다.  
- 재귀(recursive) 방식으로 정의할 수도 있다.  
- 이름 충돌을 피해야 하며, 같은 문장 안에서 이름은 유일해야 한다.

---

## 3. 구문 규칙
- `WITH` 절은 `SELECT`, `UPDATE`, `DELETE` 등 앞에 위치.  
- 여러 개 정의 시 쉼표(,)로 구분.  
- CTE 안에서 앞선 CTE는 참조할 수 있으나 뒤에 정의된 CTE는 참조 불가.

---

## 4. 컬럼 이름
- `(col1, col2, …)`로 지정 가능.  
- 지정하지 않으면 첫 번째 `SELECT`의 컬럼 명을 따른다.

---

## 5. CTE vs 파생 테이블
- **공통점**: 둘 다 임시 결과 집합.  
- **차이점**:  
  - 파생 테이블은 한 번만 참조 가능, CTE는 여러 번 참조 가능.  
  - 파생 테이블은 재귀 불가, CTE는 재귀 가능.  

---

## 6. 사용 목적
- 복잡한 쿼리를 나누어 가독성 향상.  
- 동일한 결과 집합을 반복 사용.  
- 계층 구조 등 재귀적 계산 처리.





<br>

<br>

---

# 3️⃣ 실습 문제

**두 문제 중에서 한 문제는 SubQuery와 CTE를 사용한 방법을 각각 활용해서 2개의 답변을 제시해주세요**

## 프로그래머스 문제 

https://school.programmers.co.kr/learn/courses/30/lessons/131123

> 즐겨찾기가 가장 많은 식당 정보 출력하기 (GROUP BY, SubQuery) : Lev 3

https://school.programmers.co.kr/learn/courses/30/lessons/131115

> 가격이 제일 비싼 식품의 정보 출력하기 (SUM, MAX, MIN, SubQuery) : Lev 2



---

## 문제 인증란

<img width="1915" height="955" alt="image" src="https://github.com/user-attachments/assets/558fffdc-18e6-4bdc-b18b-10bec7b400e8" />


<img width="1920" height="997" alt="image" src="https://github.com/user-attachments/assets/e43644a4-0bbe-48a8-a93f-0635ff9042d9" />


---


## 문제 1

> **🧚예린이는 최근 여러 주문 데이터를 분석하는 업무를 맡게 되었습니다. 특정 고객의 주문 이력을 분석하기 위해, 다음과 같이 최근 30일간 주문만 필터링한 CTE를 사용해 쿼리를 작성했습니다.**

~~~sql
WITH RecentOrders AS (
  SELECT *
  FROM Orders
  WHERE order_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY)
)
SELECT customer_id, COUNT(*) AS recent_order_count
FROM RecentOrders
GROUP BY customer_id;
~~~

> **그런데 예린이는 "이 쿼리를 WITH 없이, 서브쿼리 방식으로 바꿔서 실행해보라" 는 피드백을 받았고, 서브쿼리로 작성해보려 했지만 익숙하지 않아 SQL_ADVANCED를 듣는 학회원분들에게 도움을 요청하고 있습니다. 예린이의 쿼리를 WITH 없이 서브쿼리로 변환해보세요. 그리고 두 방식의 차이점을 설명해보고, 각각의 장단점을 정리해보세요**



~~~
SELECT customer_id, COUNT(*) AS recent_order_count
FROM (
  SELECT *
  FROM Orders
  WHERE order_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY)
) AS RecentOrders
GROUP BY customer_id;

## CTE (WITH) 와 서브쿼리의 차이점

- **위치와 표현 방식**
  - CTE는 쿼리 상단에 `WITH ... AS (...)` 형태로 정의하고, 이후 본문에서 이름을 참조한다.
  - 서브쿼리는 `FROM` 절이나 `WHERE` 절 등 쿼리 내부에 직접 작성한다.

- **재사용 가능 여부**
  - CTE는 한 번 정의한 뒤 같은 쿼리 안에서 여러 번 재사용할 수 있다.
  - 서브쿼리는 재사용이 불가능하며, 동일한 로직을 쓰려면 반복해서 적어야 한다.

- **가독성**
  - CTE는 로직을 단계별로 분리할 수 있어 복잡한 쿼리일수록 읽기 쉽다.
  - 서브쿼리는 중첩이 많아질수록 읽기 어렵다.

- **성능 처리 방식**
  - CTE는 DBMS에 따라 중간 결과를 임시 테이블처럼 만들어 성능이 떨어질 수 있다.
  - 서브쿼리는 옵티마이저가 인라인 뷰로 합쳐 최적화할 때 성능상 유리할 수 있다.

---

## CTE의 장단점

- 장점
  - 복잡한 쿼리를 단계별로 나눌 수 있어 이해하기 쉽다.
  - 한 번 정의하면 여러 곳에서 재사용할 수 있다.
  - 디버깅 시 각 CTE를 따로 실행해 확인하기 좋다.

- 단점
  - 일부 DBMS에서는 항상 물리적 결과를 생성하여 성능 저하가 발생할 수 있다.
  - 단순한 쿼리에서는 오히려 불필요하게 길어진다.

---

## 서브쿼리의 장단점

- 장점
  - 간단한 로직일 경우 짧고 직관적으로 표현할 수 있다.
  - 최적화 엔진이 인라인 처리하여 성능상 이점이 있을 수 있다.

- 단점
  - 같은 로직을 여러 번 쓰면 반복 작성해야 한다.
  - 쿼리가 복잡해질수록 가독성이 떨어진다.
  - 부분 실행이나 디버깅이 어렵다.

~~~



## 참고자료

서브쿼리를 사용하는 이유가 너무 어려우신 분들을 위해 참고자료를 첨부합니다. 아래 블로그를 통해서 더욱 쉽게 공부해보시고 문제를 풀어보세요.

1. [SQL] 서브쿼리는 언제 쓰는걸까? 
   https://project-notwork.tistory.com/38

2. [SQLD] 서브 쿼리 (SubQeury) 개념 및 종류
   https://bommbom.tistory.com/entry/%EC%84%9C%EB%B8%8C-%EC%BF%BC%EB%A6%ACSub-Query-%EA%B0%9C%EB%85%90-%EB%B0%8F-%EC%A2%85%EB%A5%98


### 🎉 수고하셨습니다.
