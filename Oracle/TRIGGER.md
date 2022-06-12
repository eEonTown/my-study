# TRIGGER
- 테이블에 DML문에 의해 변경사항(이벤트)이 생길 때 매번 실행할 내용을 미리 정의해둘 수 있는 객체 입니다.

# 트리거 분류
### sql문 실행 시기에 따른 분류
- BEFORE : DML문 실행 전 트리거 먼저 실행
- AFTER : DML문 실행 후 트리거 실행
### 실행시 영향을 받는 곳에 따른 분류
- ROW(행 트리거) : 실행된 트리거가 ROW하나하나 마다 실행
- STATEMENT(문장 트리거) : 실행된 트리거가 DML문장에 1번만 실행

<br>

# 생성구문
```sql
CREATE [OR REPLACE] TRIGGER 트리거명
AFTER,BEFORE DML문 ON 테이블명 -- DML문 OR사용해서 여러개 가능 UPDATE OR DELETE
[FOR EACH ROW] -- 생략시 STATEMENT
DECLARE
    선언부;
BEGIN
    실행내용;(이벤트 발생시 실행할 구문)
END;
/
```