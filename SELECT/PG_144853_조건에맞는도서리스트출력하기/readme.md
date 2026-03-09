# PG_144853 - 조건에 맞는 도서 리스트 출력하기

## 1️⃣ 문제 요약

`BOOK` 테이블에서 **카테고리가 '인문'이고 출판 연도가 2021년인 도서의 정보**를 조회하는 문제이다.

정렬 기준은 다음과 같다.

* 출판일(`PUBLISHED_DATE`) 기준 **오름차순**

출력 컬럼은 다음과 같다.

* `BOOK_ID`
* `PUBLISHED_DATE` (날짜 형식 `YYYY-MM-DD`)

---

## 2️⃣ 사용 데이터

| 컬럼명            | 설명      |
| -------------- | ------- |
| BOOK_ID        | 도서 ID   |
| CATEGORY       | 도서 카테고리 |
| PUBLISHED_DATE | 출판일     |

---

## 3️⃣ 풀이 전략

### Step 1. 조회 컬럼 선택

```sql
SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
```

문제에서 요구하는 출력 컬럼은 다음과 같다.

* `BOOK_ID`
* `PUBLISHED_DATE`

`PUBLISHED_DATE`는 `DATETIME` 형식이므로
`DATE_FORMAT()`을 사용하여 **날짜(YYYY-MM-DD)만 출력**하도록 변환한다.

---

### Step 2. 테이블 지정

```sql
FROM BOOK
```

도서 정보가 저장된 테이블은 `BOOK`이다.

---

### Step 3. 조건 설정

```sql
WHERE CATEGORY = '인문'
AND YEAR(PUBLISHED_DATE) = 2021
```

조회 조건은 다음과 같다.

* `CATEGORY`가 **'인문'**
* `PUBLISHED_DATE`의 **연도가 2021년**

`YEAR()` 함수를 사용하여 출판 연도를 필터링한다.

---

### Step 4. 출판일 기준 정렬

```sql
ORDER BY PUBLISHED_DATE ASC
```

출판일이 **빠른 순서부터 조회**해야 하므로
`PUBLISHED_DATE` 기준 **오름차순(ASC)** 정렬을 적용한다.

---

## 4️⃣ 최종 SQL

```sql
SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
FROM BOOK
WHERE CATEGORY = '인문'
AND YEAR(PUBLISHED_DATE) = 2021
ORDER BY PUBLISHED_DATE ASC;
```

---

## 5️⃣ 실행 흐름 (SQL 처리 순서 기준 사고 과정)

1️⃣ **FROM** → `BOOK` 테이블 선택

2️⃣ **WHERE**

* `CATEGORY = '인문'`
* `YEAR(PUBLISHED_DATE) = 2021`

조건에 맞는 데이터 필터링

3️⃣ **SELECT**

* `BOOK_ID`
* `DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d')`

출판일을 날짜 형식으로 변환하여 조회

4️⃣ **ORDER BY**

* `PUBLISHED_DATE` 기준 **오름차순 정렬**

---

📌 **배운 점**

* `DATE_FORMAT()`을 사용하면 `DATETIME`에서 **날짜만 출력**할 수 있다.
* `YEAR()` 함수를 사용하면 **특정 연도 데이터를 쉽게 필터링**할 수 있다.
* `ORDER BY`를 통해 **출판일 기준 정렬**이 가능하다.

---
