# GROUP BY절
- 그룹기준을 제시하는 구문 입니다.
- 여러개의 값들을 여러 그룹으로 묶어서 처리할 목적으로 사용됩니다.
```sql
SELECT *
FROM TEST
GROUP BY 그룹으로 묶을 컬럼명;
```

<br>

### 여러 컬럼 기술 가능
- GROUP BY 절에 여러 컬럼을 제시할 수 있습니다
```sql
SELECT *
FROM TEST
GROUP BY 컬럼명1, 컬럼명2 <- 컬럼1이면서 컬럼2인
```

<br>
<br>

# HAVING절
- GROUP BY절로 묶인 값중 WHERE절 처럼 특정 조건을 추가 합니다.
- HAVING절은 주로 그룹함수식을 가지고 조건을 제시할 때 사용 합니다.
```sql
SELECT *
FROM TEST
GROUP BY 컬럼명
HAVING 그룹함수를 사용한 조건식;
```