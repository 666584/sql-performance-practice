### 프로그래머스 **PG_133024 - 인기있는 아이스크림**

---

## 1️⃣ 문제 요약

`FIRST_HALF` 테이블에서
총 주문량이 많은 아이스크림의 **맛(FLAVOR)** 을 조회하는 문제이다.

정렬 기준은 다음과 같다.

1. **총 주문량(TOTAL_ORDER)** 기준 **내림차순**
2. 주문량이 같다면 **출하 번호(SHIPMENT_ID)** 기준 **오름차순**

출력 컬럼은 **FLAVOR** 이다.

---

## 2️⃣ 사용 데이터

| 컬럼명           | 설명      |
| ------------- | ------- |
| `FLAVOR`      | 아이스크림 맛 |
| `TOTAL_ORDER` | 총 주문량   |
| `SHIPMENT_ID` | 출하 번호   |

---

## 3️⃣ 풀이 전략

### Step 1. 조회 컬럼 선택

```sql
SELECT FLAVOR
```

문제에서 요구하는 출력 컬럼은 **아이스크림 맛(FLAVOR)** 이다.

---

### Step 2. 테이블 지정

```sql
FROM FIRST_HALF
```

데이터가 저장된 테이블은 `FIRST_HALF` 이다.

---

### Step 3. 주문량 기준 정렬

```sql
ORDER BY TOTAL_ORDER DESC
```

총 주문량이 많은 아이스크림부터 조회해야 하므로 **내림차순(DESC)** 으로 정렬한다.

---

### Step 4. 주문량이 같을 경우 출하 번호 기준 정렬

```sql
, SHIPMENT_ID ASC
```

주문량이 같은 경우 **출하 번호가 작은 것부터** 나오도록 **오름차순(ASC)** 정렬한다.

---

## 4️⃣ 최종 SQL

```sql
SELECT FLAVOR
FROM FIRST_HALF
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID ASC;
```

---

## 5️⃣ 실행 흐름 (SQL 처리 순서 기준 사고 과정)

1. **FROM** → `FIRST_HALF` 테이블 선택
2. **SELECT** → `FLAVOR` 컬럼 조회
3. **ORDER BY** →

   * `TOTAL_ORDER` 내림차순 정렬
   * 주문량이 같으면 `SHIPMENT_ID` 오름차순 정렬

---

📌 **배운 점**

* `ORDER BY` 에 여러 컬럼을 넣으면 **우선순위 정렬**이 가능하다.
* `DESC` 와 `ASC` 를 함께 사용하여 **복합 정렬 기준**을 만들 수 있다.
* 정렬 기준은 **왼쪽 컬럼부터 우선 적용**된다.
