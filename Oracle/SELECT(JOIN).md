# JOIN
- 두 개 이상의 테이블에서 데이터를 조회하고자 할 때 사용되는 구문 입낟.
> JOIN은 크게 오라클전용구문과 ANSI구문이 있습니다.

<br>

### JOIN분류
- INNER JOIN
- OUTER JOIN (LEFT, RIGHT)
- CROSS JOIN
- FULL OUNTER JOIN
> INNER JOIN과 OUTER JOIN은 가장 많이 사용해서 오라클전용구문과 ANSI구문을 모두 숙지하는게 좋습니다.

<br>

### INNER JOIN
- 연결시키는 컬럼의 값이 일치하는 행들만 조인되서 조회 합니다.

<br>

##### ORACLE구문
```sql
-- 두 테이블의 조인 컬럼명이 다를 때
SELECT *
FROM EMPLOYEE, DEPARTMENT
WHERE DEPT_ID = DEPT_CODE;
```
```sql
-- 두 테이블의 조인 컬럼명이 같을 때
SELECT *
FROM EMPLOYEE A, DEPARTMENT B
WHERE A.DEPT_ID = B.DEPT_ID;
```
위의 예제를 ANSI구문으로 바꾸면 아래와 같습니다.
<br>

##### ANSI구문
```sql
-- 두 테이블의 조인 컬럼명이 다를 때
SELECT *
FROM EMPLOYEE
JOIN DEPARTMENT ON (DEPT_ID = DEPT_CODE);
```
```sql
-- 두 테이블의 조인 컬럼명이 같을 때
-- 방법01
SELECT *
FROM EMPLOYEE
JOIN DEPARTMENT USING (DEPT_ID);

-- 방법02
SELECT *
FROM EMPLOYEE A
JOIN DEPARTMENT B ON (A.DEPT_ID = B.DEPT_ID);
```

<br>

### OUTER JOIN
- LEFT, RIGHT를 지정해 두 테이블간의 JOIN시 일치하지 않는 행도 포함시켜서 조회합니다.

<br>

##### ORACLE구문
```sql
SELECT *
FROM EMPLOYEE, DEPARTMENT
WHERE DEPT_ID = DEPT_CODE(+);
```

##### ANSI구문
```sql
SELECT *
FROM EMPLOYEE
LEFT JOIN DEPARTMENT ON (DEPT_ID = DEPT_CODE);
```
- LEFT : 왼쪽의 테이블이 메인테이블이 됩니다.
- RIGHT : 오른쪽의 테이블이 메인테이블이 됩니다.
JOIN테이블의 값이 존재하지 않아도 메인 테이블의 데이터가 조회되고, JOIN테이블의 값을 가져오지 못하면 NULL로 표시 됩니다.