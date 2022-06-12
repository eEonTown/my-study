# PL/SQL
- 오라클 자체에 내장 되어있는 절차적인 언어입니다.
- SQL문 내에서 변수 정의, 조건처리, 반복처리 등을 지원해서 SQL문 단점을 보완 합니다
- BLOCK구조로 다수의 SQL문을 실행 가능 합니다.
```sql
BEGIN
    DBMS_OUTPUT.OUT_LINE('HELLO');
END;
/
```

<br>

- 출력문만 작성 하면 출력창에 문구가 출력되지 않습니다.
아래 구문을 실행하면 출력 됩니다.
```sql
SET SERVEROUTPUT ON;
```

<br>

### PL/SQL구조
> 총 3가지 구조가 있습니다 선언부, 실행부, 예외처리부
- 선언부 : DECLARE로 시작하고 변수나 상수를 선언, 초기화 합니다.
- 실행부 : BEGIN으로 시작하고 로직을 기술합니다.
- 예외처리부 : EXCEPTION으로 시작하고 예외처리를 합니다.

<br>

### 선언부
```sql
DECLARE
    변수명 자료형;
    변수명 자료형 := 값
    상수명 CONSTANT 자료형 := 상수값;
BEGIN
    변수명 := 값; -- 변수 초기화
    변수명 := &입력유도문 -- 사용자에게 입력받음

    DBMS_OUTPUT.OUT_LINE() -- 출력문
END;
/
```

<br>

##### 레퍼런스 타입 변수 선언, 초기화
```sql
DECLARE
    변수명 참조테이블.참조컬럼%TYPE; -- 참조한 컬럼의 타입으로 지정
BEGIN
    SELECT 컬럼, 컬럼, 컬럼
    INTO 변수명, 변수명, 변수명
    FROM 테이블명
    WHERE 조건식 -- 조회된 결과를 변수에 담을 수 있습니다.
END;
/
```

<br>

##### ROW타입 변수 선언
```sql
DECLARE
    변수명 참조테이블%ROWTYPE;
BEGIN
    SELECT *
    INTO 변수명
    FROM 테이블명
    WHERE 조건식 -- 한 행의 데이터를 담을 수 있습니다.

    DBMS_OUTPUT.PUT_LINE(변수명.컬럼명);
END;
/
```

<br>

### 실행부
##### IF문
```sql
DECLARE
    구문
BEGIN
    SELECT 컬럼명
    INTO 변수명
    FROM 테이블명
    WHERE 조건식
    
    IF 조건식
    THEN 실행문
    ELSE 실행문
    END IF;
END;
/
```
```sql
DECLARE
    구문
BEGIN
    SELECT 컬럼명
    INTO 변수명
    FROM 테이블명
    WHERE 조건식
    
    IF 조건식
    ELSIF 실행문
    ELSE 실행문
    END IF;
END;
/
```
##### CASE문
```sql
DECLARE
    구문
BEGIN
    SELECT 컬럼명
    INTO 변수명
    FROM 테이블명
    WHERE 조건식
    
    변수 := CASE 비교대상자
                WHEN 비교값 THEN 반환값
                ELSE 반환값
            END;
END;
/
```
##### LOOP문
