# 프로그래머스 151136 - 평균 일일 대여 요금 구하기

## 1️⃣ 문제 요약

`CAR_RENTAL_COMPANY_CAR` 테이블에서  
**SUV 차량만 조회하여 평균 일일 대여 요금(daily_fee)을 구하는 문제**이다.

- 평균값은 **반올림하여 정수로 출력**
- 출력 컬럼명은 `AVERAGE_FEE`

---

## 2️⃣ 사용 데이터

- `car_type` : 차량 종류 (SUV 여부 확인)
- `daily_fee` : 일일 대여 요금 (평균 계산 대상)

---

## 3️⃣ 풀이 전략

### Step 1. SUV 차량만 필터링

```sql
WHERE car_type = 'SUV'
```

문자열 비교 시 작은따옴표 ' ' 사용이 표준적이며 안전하다.
더블쿼트 " " 는 DB 설정에 따라 다르게 동작할 수 있다.

### Step 2. 평균 계산
AVG(daily_fee)

집계 함수 AVG()를 사용하여 평균값을 계산한다.

### Step 3. 반올림 처리
ROUND(AVG(daily_fee), 0)

두 번째 인자 0 → 소수점 없이 정수로 반올림

### Step 4. 컬럼명 지정
AS AVERAGE_FEE

출력 컬럼 이름을 문제 요구사항에 맞게 지정한다.

---

## 4️⃣ 최종 SQL
SELECT ROUND(AVG(daily_fee), 0) AS AVERAGE_FEE
FROM CAR_RENTAL_COMPANY_CAR
WHERE car_type = 'SUV';

---

## 5️⃣ 실행 흐름 (SQL 처리 순서 기준 사고 과정)

FROM → 테이블 선택

WHERE → SUV 차량만 필터링

AVG → 필터링된 데이터의 평균 계산

ROUND → 평균값 반올림

SELECT → 결과 출력 및 별칭 적용

---

## 📌 배운 점

문자열 비교는 작은따옴표 사용이 표준이다.

집계 함수는 WHERE 조건 이후의 데이터에 대해 적용된다.

ROUND 함수의 자리수를 명시하는 것이 안전하다.
