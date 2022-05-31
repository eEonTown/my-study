# 함수 Function
- 특정 내용을 수행시킨 후 실행한 결과를 반환합니다.
- 함수를 기술할 수 있는 위치는 SELECT, WHERE, ORDER BY, GROUP BY, HAVING, DML등 입니다.

<br>

### LENGTH, LENGTHB 문자 처리 함수
- LENGTH(문자열) : 글자수를 반환
- LENGTHB(문자열) : 바이트수를 반환
> 한글은 한글자에 3바이트, 영문,숫자, 특수문자는 1바이트 입니다.

<br>

### INSTR, SUBSTR
- INSTR(문자열, 찾는문자, 찾을위치의시작값) : 찾는 문자의 시작위치를 반환
- SUBSTR(문자열, 시작값, 문자길이) : 범위의 특정 문자열을 추출해서 반환 문자 길이를 생략하면 끝까지 추출합니다.

##### 찾을 위치의 시작값
- 1 : 앞에서 부터 찾음(기본값)
- -1 : 뒤에서부터 찾음

<br>

### LPAD, RPAD
- 문자열을 통일감있게 조회하고자 할 때 사용합니다.
- RPAD, LPAD(문자열, 반환할문자길이, 붙힐문자) : 왼쪽, 오른쪽에 문자를 붙여서 반환할문자길이 만큼의 문자열을 반환
- 붙힐문자 생략시 기본값으로 공백이 입력됩니다.

<br>

### LTRIM, RTRIM, TRIM
- 문자열의 앞, 뒤, 양쪽에 있는 특정 문자를 제거한 나머지 문자열을 반환 합니다.
- 제거할 문자열 생략시 기본값이 공백 입니다.
```
RTRIM, LTRIM(문자열, 제거할문자열);

TRIM([LEADING, TRAILING, BOTH] '제거할문자' FRIM 문자열)
```
- LEADING : 앞
- TRAILING : 뒤
- BOTH : 양쪽

<br>

### LOWER, UPPER, INITCAP
- LOWER : 전부 소문자로 변형
- UPPER : 전부 대문자로 변형
- INITCAP : 앞 한글자만 대문자로 변형
```
LOWER, UPPER, INITCAP(문자열);
```

<br>

### REPLACE
- 특정문자열을 찾아서 특정문자로 변경시킵니다.
```
REPLACE(문자열, 찾는문자, 변경할문자)

REPLACE('Hello', 'll', 'LL');
```

<br>
<br>

# 숫자처리 함수

### ABS
- 숫자의 절대값을 구합니다.
```
ABS(숫자);
```

<br>

### MOD
- 두 수를 나누고 나머지 값을 반환합니다.
```
MOD(숫자, 숫자);
```

<br>

### ROUND, CEIL, FLOOR, TRUNC
- ROUND : 반올림 값을 반환합니다.
- CEIL : 올림 값을 반환합니다.
- FLOOR : 버림 값을 반환합니다.
- TRUNC : 위치지정 가능한 버림처리를 합니다.
```
ROUND, CEIL, FLOOR(소수);
TRUNC(소수, [소수점위치]);
```

<br>

# 날짜처리 함수

### MONTHS BETWEEN
- 두 날짜 사이의 개월수를 반환합니다.
```
MONTHS BETWEEN(날짜1, 날짜2)
```

<br>

### ADD MONTHS
- 특정 날짜에서 숫자만큼의 개월수를 더해 그 날짜를 반환합니다.
```
ADD MONTHS(날짜, 개월수)
```

<br>

### NEXT_DAY, LAST_DAY
- NEXT_DAY : 해당 날짜에서 가까운 요일의 날짜를 반환
- LAST_DAY : 해당 월의 마지막 날짜를 반환
```
NEXT_DAY(날짜, 요일)
LAST_DAY(날짜)
```

<br>

### EXTRACT
- 특정 날짜를 년, 월, 일로 값을 추출해서 반환합니다.
```
EXTRACT(YEAR FROM 날짜);
EXTRACT(MONTH FROM 날짜);
EXTRACT(DAY FROM 날짜);
```

<br>
<br>

# NULL 처리 함수

### NVL
- 해당 컬럼에 NULL값이 존재할 경우 지정한반환값을 반환합니다.
```
NVL(컬럼명, NULL일때반환값);
```

<br>

### NVL2
- 해당 컬럼값이 존재할 경우 반환값1 반환, NULL일 경우 반환값2 반환
```
NVL2(컬럼명, 반환값1, 반환값2);
```

<br>

### NULLIF
- 두 개의 값이 일치하면 NULL반환, 일치하지 않으면 비교대상1 값 반환
```
NULLIF(비교대상1, 비교대상2)
```

<br>
<br>

# 선택 함수

### DECODE
- Java에서 Switch문과 비슷한 개념 입니다.
```
DECODE(비교대상컬럼명, 비교값1, 결과값1, 비교값2, 결과값2, ..., [결과값]);
```

<br>

### CASE WHEN THEN
```
CASE WHEN 조건식1 THEN 결과값1
     WHEN 조건식2 THEN 결과값2
     ...
     ELSE 결과값
END [AS 별칭가능]
```

<br>
<br>

# 그룹 함수

### SUM, AVG
- SUM : 해당 컬럼 값의 총합을 구해서 반환합니다.
- AVG : 해당 컬럼 값의 평균을 구해서 반환합니다.
```
SUM, AVG(NUMBER타입컬럼);
```

<br>

### MAX, MIM
- MAX : 컬럼에서 가장 큰 값을 반환합니다.
- MIN : 컬럼에서 가장 작은 값을 반환합니다.
```
MAX, MIN(NUMBER타입컬럼);
```

<br>

### COUNT
- 해당 컬럼의 행 수를 반환합니다.
- NULL값은 포함하지 않습니다. NULL값도 포함하기 위해서는 NVL함수를 응용 합니다.
```
COUNT(*)
COUNT(컬럼명)
COUNT(DISTINCT 컬럼명)
```

<br>
<br>

# 형 변환 함수

### TO_CHAR
- 숫자타입, 날짜타입의 값을 문자타입으로 변환시켜주는 함수 입니다.

<br>

##### 숫자타입 => 문자타입
```
TO_CHAR(1234, '99999') --빈칸을 공백으로 채웁니다.
TO_CHAR(1234, '00000') --빈칸을 0으로 채웁니다.
TO_CHAR(1234, 'L99999') --현재 설정된 나라의 화폐단위
TO_CHAR(100000000, 'L999,999,999') --빈칸을 0으로 채웁니다.
```

<br>

##### 날짜타입 => 문자타입
```
TO_CHAR(날짜, 'YYYY-MM-DD DAY');
TO_CHAR(날짜, 'HH24-MI-SS'); --24시간형식, 12시간형식, AM, PM
TO_CHAR(날짜, 'YY-FMMM-DD'); --FM은 0을 없애줍니다.
TO_CHAR(날짜, 'YYYY"년", MM"월", DD"일" (DAY)) -- 0000년 00월 00일 0요일
```
- 연도 : YYYY, RRRR, YY, RR, YEAR
- 월 : MM, MON, MONTH, RM
- 일 : DDD, DD, D
- 요일 : DAY, DY

<br>

### TO_DATE
- 숫자타입, 문자타입의 값을 날짜타입으로 변환시켜주는 함수입니다.
```
TO_DATE(19970804);
TO_DATE(970804);
TO_DATE('970804');

SELECT TO_DATE('041030 143030', 'YYMMDD HH24MISS')

TO_DATE(970804, 'YYMMDD');
TO_DATE(970804, 'RRMMDD');
```
> 연도에서 YY는 무조건 현재세기로 반영됩니다 EX) 2078년
> RR은 년도값이 50미만일 경우 현재세기반영 이상일 경우 이전 세기반영 EX) 1978년

<br>

### TO_NUMBER
- 문자타입의 값을 숫자타입으로 변환시켜주는 함수입니다.
```
TO_NUMBER(문자, [포맷]);

TO_NUMBER('1,000,000', '9,999,999')

TO_NUMBER(1,000,000', '9,999,999') + TO_NUMBER('500,000', '999,999'); -- 1500000
```