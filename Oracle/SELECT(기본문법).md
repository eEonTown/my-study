# SELECT문
- 데이터를 조회할 때 사용되는 구문

<br>

### SELECT 기본 표현법
```sql
SELECT 조회할컬럼1, 조회할컬럼2, ...
FROM 조회할테이블명;
```
- 모든 컬럼을 조회하려면 SELECT절에 *를 입력하면 됩니다.
- SELECT문에서 산술연산식 기술이 가능합니다.

<br>

### 컬럼명 별칭 지정 4가지 방법
- 컬럼명 별칭
- 컬럼명 AS 별칭
- 컬럼명 "별칭"
- 컬럼명 AS "별칭"
> 별칭에 공백이나 특수문자가 포함될경우 ""로 기술해야 합니다.

<br>

### 연결 연산자
> java에서 System.out.println("안녕 나는" + name + "이야"); 같은 개념 입니다.
- Oracle에서는 + 대신 ||를 사용 합니다.

<br>

### DISTINCT
- 컬럼에 중복된 값들을 한번만 조회합니다.
- DISTINCT는 한번만 사용 가능합니다 중복사용 하려면 ,로 묶어 사용 가능합니다.
```sql
SELECT DISTINCT 컬럼명
FROM 테이블명;

SELECT DISTINCT 컬럼명, 컬럼명
FROM 테이블명;
```

<br>
<br>

# WHERE절
- 특정 조건의 데이터만 조회하고자 할 때 사용합니다.

<br>

### WHERE 표현법
-　>, <, <=, >=, =, !=, IS NULL, IS NOT NULL 사용 가능합니다.
- NULL 값은 IS NULL, IS NOT NULL을 사용합니다.
```sql
SELECT 조회할컬럼1, 조회할컬럼2, ...
FROM 조회할테이블명
WHERE 조건식;
```

<br>

### 논리연산자
- 조건을 묶어서 제시 합니다.
- AND (모든 조건 포함, ~이면서, 그리고)
- OR (조건 따로따로 ~이거나, 또는)
```sql
SELECT 조회할컬럼1, 조회할컬럼2, ...
FROM 조회할테이블명
WHERE 조건식
AND, OR
AND, OR
...
```

<br>

### BETWEEN AND
- WHERE절 조건식에서 사용되는 구문 입니다.
- 범위에 대한 조건을 제시할 때 사용됩니다.
```sql
SELECT 조회할컬럼1, 조회할컬럼2, ...
FROM 조회할테이블명
WHERE 비교대상컬럼 BETWEEN 하한값 AND 상한값;

WHERE MONEY BETWEEN 3000000 AND 50000000;
```

<br>

### LIKE
- 비교대상의 컬럼값이 내가 제시한 특정 패턴에 만족할 경우 조회 합니다.
```sql
SELECT 조회할컬럼1, 조회할컬럼2, ...
FROM 조회할테이블명
WHERE 비교대상컬럼 LIKE '제시할패턴'
```

##### 제시할패턴
- '문자%' : 비교대상의 컬럼값이 해당 문자로 시작될 경우 조회
- '%문자' : 비교대상의 컬럼값이 해당 문자로 끝날 경우 조회
- '%문자%' : 비교대상의 컬럼값에 해당 문자가 포함될 경우 조회
- '_문자' : 두번째 자리가 문자일 경우 조회(_하나당 1글자 입니다.)

##### ESCAPE
- 제시할패턴이 인식하지 못하는 특정 문자를 사용하고싶을 때 작성합니다.
```sql
비교대상컬럼 LIKE '__$_%' ESCAPE '$';
```

<br>

### IN
- 비교대상컬럼값이 내가 제시한 목록중에 일치하는 값이 있는지 확인 후 조회합니다.
```sql
SELECT 조회할컬럼1, 조회할컬럼2, ...
FROM 조회할테이블명
WHERE 비교대상컬럼 IN (값, 값, 값, ...);
```

<br>

### ORDER BY
- 지정컬럼의 데이터를 오름차순 또는 내림차순으로 정렬 합니다.
- ORDER BY절은 SELECT문 가장 마지막 줄에 작성하며, 실행 순서 또한 마지막 입니다.
```sql
SELECT 조회할컬럼1, 조회할컬럼2, ...
FROM 조회할테이블명
WHERE 조건식
ORDER BY 지정컬럼 OR 별칭 OR 컬럼순번 [ASC, DESC] [NULLS FIRST, NULLS LAST]

ORDER BY MONEY DESC NULLS FIRST;
```
- [] 대괄호는 생략가능 구문 입니다.
- ASC : 오름차순 정렬 (기본값)
- DESC : 내림차순 정렬
- NULLS FIRST : NULL값을 앞에 정렬
- NULLS LAST : NULL값을 뒤에 정렬