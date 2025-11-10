# SQL_ADVANCED 5주차 정규 과제 

## Week 5 : 계층형 질의 & 셀프 조인

📌**SQL_ADVANCED 정규과제**는 매주 정해진 주제에 따라 **MySQL 공식 문서 또는 한글 블로그 자료를 참고해 개념을 정리한 후, 프로그래머스 SQL 문제 3문제**와 **추가 확인문제**를 직접 풀어보며 학습하는 과제입니다. 

이번 주는 아래의 **SQL_ADVANCED_5th_TIL**에 나열된 주제를 중심으로 개념을 학습하고, 주차별 **학습 목표**에 맞게 정리해주세요. 정리한 내용은 GitHub에 업로드한 후, **스프레드시트의 'SQL' 시트에 링크를 제출**해주세요. 



**(수행 인증샷은 필수입니다.)** 

> 프로그래머스 문제를 풀고 '정답입니다' 문구를 캡쳐해서 올려주시면 됩니다. 



## SQL_ADVANCED_5th

### 15.2.20 WITH (Common Table Expressions)

- **재귀 CTE를 통한 계층형 구조 탐색 방법을 중심으로 학습해주세요.**

> Self Join은 따로 MySQL 공식문서가 없습니다. 다른 블로그나 유튜브 영상을 참고하여 스스로 학습하고, 넣어주세요. 



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위               | 완료 여부 |
| ----- | ----------------------- | --------- |
| 1주차 | 서브쿼리 & CTE          | ✅         |
| 2주차 | 집합 연산자 & 그룹 함수 | ✅         |
| 3주차 | 윈도우 함수             | ✅         |
| 4주차 | Top N 쿼리              | ✅         |
| 5주차 | 계층형 질의와 셀프 조인 | ✅         |
| 6주차 | PIVOT / UNPIVOT         | 🍽️         |
| 7주차 | 정규 표현식             | 🍽️         |



### 공식 문서 활용 팁

>  **MySQL 공식 문서는 영어로 제공되지만, 크롬 브라우저에서 공식 문서를 열고 이 페이지 번역하기에서 한국어를 선택하면 번역된 버전으로 확인할 수 있습니다. 다만, 번역본은 문맥이 어색한 부분이 종종 있으니 영어 원문과 한국어 번역본을 왔다 갔다 하며 확인하거나, 교육팀장의 정리 예시를 참고하셔도 괜찮습니다.**



# 1️⃣ 학습 내용

> 아래의 링크를 통해 *MySQL 공식문서*로 이동하실 수 있습니다.
>
> - 15.2.20 WITH (Common Table Expressions) : MySQL 공식문서 
>
> https://dev.mysql.com/doc/refman/8.0/en/with.html
>
> (한국어 버전) https://dart-b-official.github.io/posts/mysql-RecursiveWith/



<br>

---

# 2️⃣ 학습 내용 정리하기

## 1. 계층형 질의 (WITH RECURSIVE)

~~~
✅ 학습 목표 :
* 'WITH RECURSIVE' 문법을 활용해 계층형 구조를 탐색할 수 있다.
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->



## 2. 셀프 조인

~~~
✅ 학습 목표 :
* 같은 테이블 내에서 상호 관계를 탐색할 수 있는 셀프 조인의 구조를 이해하고 사용할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->
1. 계층형 질의 (WITH RECURSIVE)
WITH RECURSIVE는 공통 테이블 표현식(CTE) 중 자기 자신을 참조하는 형태를 의미한다.
즉, 하나의 임시 테이블(CTE)이 자신의 결과를 다시 참조하여 반복적으로 데이터를 확장한다.

기본 구조 예시:

WITH RECURSIVE cte (n) AS (
  SELECT 1              -- 비재귀(시드) 부분
  UNION ALL
  SELECT n + 1 FROM cte -- 재귀 부분
  WHERE n < 5
)
SELECT * FROM cte;


결과

+---+
| n |
+---+
| 1 |
| 2 |
| 3 |
| 4 |
| 5 |
+---+
🧩 구조와 규칙
구분	설명
비재귀(시드) SELECT	초기 데이터 생성. CTE를 참조하지 않음.
재귀 SELECT	CTE 자신을 참조하여 이전 결과를 기반으로 다음 단계 생성.
종료 조건	재귀 SELECT가 더 이상 새로운 행을 생성하지 못하면 자동 종료됨.
형식 제약	자기참조 시 반드시 WITH RECURSIVE를 사용해야 함.

⚙️ 재귀 CTE의 동작 방식

UNION ALL 또는 UNION DISTINCT로 비재귀와 재귀 부분을 연결한다.

각 반복(iteration)은 직전 단계에서 생성된 행만을 입력으로 사용한다.

재귀 SELECT 내부에서는 다음을 사용할 수 없음:

집계 함수 (SUM, AVG, …)

윈도 함수

GROUP BY, ORDER BY, DISTINCT

(MySQL 8.0.19 이전) LIMIT


⚠️ 주의 및 성능 팁
항목	설명
재귀 깊이 제한	cte_max_recursion_depth (기본 1000)으로 제어
실행 시간 제한	max_execution_time 또는 MAX_EXECUTION_TIME 힌트 사용
무한 루프 방지	종료 조건 명시, LIMIT 활용
성능 최적화	메모리 임시 테이블 한도 증가 시 속도 개선 가능
🔍 CTE vs 파생 테이블(Subquery)
구분	CTE (WITH)	파생 테이블
재사용 가능성	여러 번 참조 가능	1회만 사용 가능
자기참조	가능 (재귀 CTE)	불가능
가독성	높음 (쿼리 선두부 정의)	상대적으로 낮음
생성 권한 필요 여부	불필요	CREATE TEMP TABLE 권한 필요할 수 있음


✅ 학습 목표:

WITH RECURSIVE 문법을 활용해 계층형 구조(조직도, 트리, 카테고리 등) 를 탐색할 수 있다.

📘 개요

WITH RECURSIVE는 공통 테이블 표현식(CTE) 중 자기 자신을 참조하여
반복적으로 데이터를 생성하거나 누적 처리하는 문법이다.
일반적으로 순차적 데이터 생성, 경로 탐색, 누적 합산, 그래프 탐색 등에 사용된다.

🧩 기본 구조

비재귀(시드) 부분: 최초 한 번만 실행되어 초기 데이터를 만든다.

재귀 부분: 바로 이전 단계의 결과를 입력으로 받아, 조건이 만족될 때까지 반복 실행된다.

두 부분은 UNION ALL 또는 UNION DISTINCT로 결합된다.

⚙️ 주요 규칙
구분	설명
문법 키워드	자기참조가 포함된 경우 반드시 WITH RECURSIVE로 시작해야 한다.
타입 결정	열 타입은 비재귀 부분 기준으로 결정되며, 모든 열은 NULL 허용으로 간주된다.
UNION ALL / DISTINCT	UNION ALL은 중복 허용, UNION DISTINCT는 중복 제거로 무한 루프 방지 가능.
반복 입력 원리	매 반복(iteration)은 직전 결과 집합을 입력으로 사용한다.
⚠️ 문법 제약

재귀 SELECT 내부에서는 다음 문법이 제한된다.

집계 함수 (SUM, AVG, COUNT 등)

윈도 함수

GROUP BY, ORDER BY, DISTINCT

(MySQL 8.0.18 이하) LIMIT 사용 불가

LEFT JOIN의 오른쪽 피연산자로 CTE를 둘 수 없음

FROM 절 내에서 CTE는 한 번만 참조 가능

🔒 안전장치 및 제한
항목	설명
재귀 깊이 제한	cte_max_recursion_depth (기본값 1000)으로 제한 가능
실행 시간 제한	max_execution_time 또는 옵티마이저 힌트 MAX_EXECUTION_TIME 사용 가능
무한 루프 방지	종료 조건(WHERE) 및 LIMIT 절로 제어
성능 관리	재귀 반복이 많으면 디스크 기반 임시 테이블로 전환될 수 있으므로 주의
🧮 CTE와 파생 테이블의 비교
구분	CTE (WITH)	파생 테이블(Subquery)
참조 횟수	여러 번 참조 가능	1회만 사용 가능
자기참조	가능 (WITH RECURSIVE)	불가능
가독성	높음 (쿼리의 논리 구조가 선두에 위치)	낮음
권한 필요 여부	명시적 생성/삭제 권한 불필요	임시 테이블 생성 시 권한 필요할 수 있음

<br>

<br>

---

# 3️⃣ 실습 문제

## 문제 

- https://leetcode.com/problems/employees-earning-more-than-their-managers/ 

> LeetCode 181. Employees  Earning More Than Their Managers
>
> 학습 포인트 : 동일 테이블을 두 번 조인 (왜 동일 테이블을 JOIN 해야하는 문제일까)

- https://leetcode.com/problems/tree-node/description/

> LeetCode 608. Tree Node 
>
> 학습 포인트 : id, parent_id 기반의 트리 구조에서 **부모 ~ 자식 관계 재귀 탐색**
>
> Hint : (문제 해석) 
>
> - 어떤 노드가 Root Node 이려면, 부모노드가 존재하지 않아야 한다. 
> - 어떤 노드가 Inner Node 이려면, 나를 부모로 가지는 노드가 하나 이상 존재하여야 한다.
>   - 그 외네는 모두 Leaf Node 이다. --> (CASE 문을 사용하는 것을 추천드립니다.)

- https://school.programmers.co.kr/learn/courses/30/lessons/144856

> 프로그래머스 : 저자 별 카테고리 별 매출액 집계하기 
>
> 학습 포인트 : 카테고리와 서브카테고리 계층 구조를 분석하는 로직, SELF JOIN / CTE를 다 활용할 수 있다.
>
> - 위에 2가지의 문제를 풀어보고 난 이후, 더 편리한 방법으로 문제를 풀어보세요.

---

## 문제 인증란

<!-- 이 주석을 지우고 여기에 문제 푼 인증사진을 올려주세요. -->
<img width="697" height="627" alt="image" src="https://github.com/user-attachments/assets/8b368cf8-8ef0-4aa0-82a9-c9f953fe2a09" />

<img width="704" height="674" alt="image" src="https://github.com/user-attachments/assets/3e7a9896-1787-479d-8421-1bbb5197792d" />

<img width="926" height="594" alt="image" src="https://github.com/user-attachments/assets/f86116b4-df1a-4790-974c-88e70d2da63c" />

---

# 확인문제

## 문제 1

> **🧚윤서는 어떤 기업의 조직 구조를 분석하는 SQL 쿼리를 작성하고 있습니다. 각 직원은 상위 관리자 ID(manager_id)를 가지며, 조직도는 같은 Employees 테이블 내에서 계층적으로 연결됩니다. 윤서는 최상위 관리자부터 각 사원까지의 계층 깊이(depth)를 계산하고자 다음과 같은 SELF JOIN 기반 쿼리를 시도했습니다.** 

~~~sql
SELECT e1.id, e1.name, e2.name AS manager_name
FROM Employees e1
LEFT JOIN Employees e2 ON e1.manager_id = e2.id;
~~~

> **쿼리를 잘 작성했다고 생각을 했지만, 막상 실행을 해보니 1단계 매니저까지만 추적할 수 있어 계층 구조의 전체를  표현하는데 한계가 존재했습니다. 이에 여러분에게 다음과 같은 미션을 요청합니다. WITH RECURSIVE를 활용하여  최상위 관리자부터 시작해 각 직원까지의 조직 구조 계층 깊이(depth)를 구하고, 결과를 depth가 높은 순으로 정렬하는 쿼리를 작성하세요.**



~~~
-- MySQL 8+, PostgreSQL, SQL Server, SQLite
WITH RECURSIVE org AS (
  -- 시드: 최상위 관리자(manager_id IS NULL)
  SELECT
    e.id,
    e.name,
    e.manager_id,
    0 AS depth,                               -- 루트 깊이 = 0 (원하면 1로 변경)
    CAST(e.id AS CHAR(200)) AS path           -- (선택) 경로 누적용
  FROM Employees e
  WHERE e.manager_id IS NULL

  UNION ALL

  -- 재귀: 직속 부하들을 한 단계씩 확장
  SELECT
    c.id,
    c.name,
    c.manager_id,
    p.depth + 1 AS depth,
    CONCAT(p.path, '>', c.id) AS path
  FROM Employees c
  JOIN org p
    ON c.manager_id = p.id
)
SELECT
  id,
  name,
  manager_id,
  depth
FROM org
ORDER BY depth DESC, id;

~~~



---

### 참고자료

<!--셀프조인에 대해 학습하시기에 도움이 되도록 참고할말한 잘 설명된 블로그들을 같이 첨부하겠습니다. -->

https://step-by-step-digital.tistory.com/101



<br>

### 🎉 수고하셨습니다.
