1) 문제 요약

CAR_RENTAL_COMPANY_CAR 테이블에서 SUV 차량만 골라서
그들의 평균 일일 대여 요금(daily_fee) 을 구한다.

평균은 반올림하여 정수로 출력

출력 컬럼명은 AVERAGE_FEE

2) 필요한 데이터

car_type : 차량 종류 (SUV인지 확인)

daily_fee : 일일 대여 요금 (평균 대상)

3) 풀이 전략
Step 1. SUV만 필터링

WHERE car_type = 'SUV'

문자열은 DB에 따라 "가 다르게 동작할 수 있어서
작은따옴표 'SUV' 사용이 가장 안전하고 표준적이다.

Step 2. 평균 계산

AVG(daily_fee)

Step 3. 반올림해서 정수로 만들기

ROUND(AVG(daily_fee), 0)

자리수 0 → 소수점 없이 정수로 반올림

Step 4. 컬럼 별칭 지정

AS AVERAGE_FEE

4) 최종 SQL
SELECT ROUND(AVG(daily_fee), 0) AS AVERAGE_FEE
FROM CAR_RENTAL_COMPANY_CAR
WHERE car_type = 'SUV';
5) 실행 흐름(사고 순서)

FROM : 테이블 선택

WHERE : SUV만 남김

AVG : 남은 행의 daily_fee 평균

ROUND : 평균값 반올림

SELECT : 결과 출력 + 별칭 적용
