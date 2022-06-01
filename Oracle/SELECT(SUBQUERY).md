# SUBQUERY
- 하나의 SQL문 안에 포함된 또다른 SELECT문을 서브쿼리라고 합니다.
- 메인 SQL문을 위해 보조 역할을 하는 쿼리문

<br>

### 단일 행 서브쿼리
- 서브쿼리의 조회 결과값 갯수가 1행 1열 입니다.
- 단일행 서브쿼리 앞에는 비교연산자를 사용할 수 있습니다.
```sql
SELECT *
FROM TEST
WHERE NUM <= (SELECT NUM
                FROM TEST
               WHERE NAME = '이름'
             );
```
<br>

### 다중 행 서브쿼리
- 서브쿼리의 조회 결과값이 여러 행 입니다. (열은 1개)
- 다중 행 서브쿼리 앞에는 일반 비교연산자를 사용할 수 없습니다.
- 연산자를 제외하면 단일 행 서브쿼리와 같습니다.
```sql
SELECT *
FROM TEST
WHERE NUM IN (SELECT NUM
                FROM TEST
               WHERE NAME IN ('이름1', '이름2')
             );
```

<br>

### 다중 열 서브쿼리
- 결과는 한 행 이지만 나열된 컬럼수가 여러개 입니다.
```sql
SELECT *
FROM TEST
WHERE NUM = (SELECT NUM
                FROM TEST
               WHERE NAME = '이름1'
             );
AND CODE = (SELECT CODE
             FROM TEST
            WHERE NAME = '이름1'
             );

-- 위 구문을 다중열 서브쿼리로 작성할 수 있습니다.
SELECT *
FROM TEST
WHERE (NUM, CODE) = (SELECT NUM, CODE
                       FROM TEST
                      WHERE = '이름1'
                    );
```

<br>

### 다중 행 다중 열 서브쿼리
- 서브쿼리 조회 결과값이 여러행이면서 여러 컬럼 입니다.
```sql
SELECT *
FROM TEST
WHERE (NUM, CODE) = (SELECT NUM, CODE
                       FROM TEST
                      GROUP BY CODE
                    );
```

### 인라인 뷰
- FROM절에서 서브쿼리를 사용
- 메인 쿼리문보다 먼저 수행 되므로 SQL문장에서 절차성을 주는 효과가 있습니다.
```sql
SELECT ROWNUM, NAME
FROM TEST
WHERE ROWNUM = 1
ORDER BY NAME;
-- ROWNUM은 FROM절을 수행하면서 붙여지기 때문에 NAME순서의 정확한 데이터를 얻기 어렵습니다.

-- 인라인 뷰를 이용해서 FROM절에 이미 정렬된 데이터를 조회합니다.
SELECT ROWNUM
FROM (SELECT *
        FROM TEST
       ORDER BY NAME)
WHERE ROWNUM = 1;
```