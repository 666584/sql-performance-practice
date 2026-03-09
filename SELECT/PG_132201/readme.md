# PG_132201 - 12세 이하인 여자 환자 목록 출력하기

## 1️⃣ 문제 요약

`PATIENT` 테이블에서 **12세 이하의 여자 환자 정보**를 조회하는 문제이다.

조회 조건은 다음과 같다.

* 나이(`AGE`)가 **12세 이하**
* 성별(`GEND_CD`)이 **여자(W)**

추가 조건

* 전화번호(`TLNO`)가 **NULL이면 'NONE'으로 표시**

정렬 기준

* 나이(`AGE`) **내림차순**
* 나이가 같다면 이름(`PT_NAME`) **오름차순**

출력 컬럼

* `PT_NAME`
* `PT_NO`
* `GEND_CD`
* `AGE`
* `TLNO`

---

## 2️⃣ 사용 데이터

| 컬럼명     | 설명    |
| ------- | ----- |
| PT_NAME | 환자 이름 |
| PT_NO   | 환자 번호 |
| GEND_CD | 성별 코드 |
| AGE     | 나이    |
| TLNO    | 전화번호  |

---

## 3️⃣ 풀이 전략

### Step 1. 조회 컬럼 선택

```sql id="jq0t8f"
SELECT PT_NAME, PT_NO, GEND_CD, AGE,
       IF(TLNO IS NULL, 'NONE', TLNO) AS TLNO
```

문제에서 요구하는 출력 컬럼은 다음과 같다.

* `PT_NAME`
* `PT_NO`
* `GEND_CD`
* `AGE`
* `TLNO`

전화번호(`TLNO`)가 `NULL`인 경우 `'NONE'`으로 출력해야 하므로
`IF()` 함수를 사용하여 값을 변환한다.

---

### Step 2. 테이블 지정

```sql id="h7xckg"
FROM PATIENT
```

환자 정보가 저장된 테이블은 `PATIENT`이다.

---

### Step 3. 조회 조건 설정

```sql id="v3rq4k"
WHERE AGE <= 12
AND GEND_CD = 'W'
```

조회 조건

* 나이(`AGE`) **12세 이하**
* 성별(`GEND_CD`) **여자(W)**

---

### Step 4. 정렬 기준 적용

```sql id="ajtdyr"
ORDER BY AGE DESC, PT_NAME ASC
```

정렬 기준

1. 나이(`AGE`) **내림차순**
2. 나이가 같으면 이름(`PT_NAME`) **오름차순**

---

## 4️⃣ 최종 SQL

```sql id="yq3p2s"
SELECT PT_NAME, PT_NO, GEND_CD, AGE,
       IF(TLNO IS NULL, 'NONE', TLNO) AS TLNO
FROM PATIENT
WHERE AGE <= 12
AND GEND_CD = 'W'
ORDER BY AGE DESC, PT_NAME ASC;
```

---

## 5️⃣ 실행 흐름 (SQL 처리 순서 기준 사고 과정)

1️⃣ **FROM** → `PATIENT` 테이블 선택

2️⃣ **WHERE**

* `AGE <= 12`
* `GEND_CD = 'W'`

조건에 맞는 환자 데이터 필터링

3️⃣ **SELECT**

* 환자 정보 컬럼 조회
* `IF(TLNO IS NULL, 'NONE', TLNO)`을 통해 **전화번호 NULL 처리**

4️⃣ **ORDER BY**

* `AGE` 내림차순
* 나이가 같으면 `PT_NAME` 오름차순

---

📌 **배운 점**

* `IF()` 함수를 사용하면 **조건에 따라 출력 값을 변경**할 수 있다.
* `NULL` 값은 `IS NULL`을 사용하여 비교해야 한다.
* `ORDER BY`에 여러 컬럼을 사용하면 **우선순위 정렬**이 가능하다.
