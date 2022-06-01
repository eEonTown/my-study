# SEQUENCE
- 순차적으로 정수 값을 자동으로 생성하는 역할을 합니다.

<br>

### 시퀀스 생성 구문
```sql
CREATE SEQUENCE 시퀀스명
[START WITH 번호시작숫자]
[INCREMENT BY 증가숫자]
[MAXVALUE 최대숫자] -- NOMAXVALUE 최대값 없음
[MINVALUE 최소숫자] -- NOMINVALUE 최소값 없음
[CYCLE, NOCYCLE] -- 최대값 도달시 시작번호로 돌아감 NOCYCLE은 에러를 발생 시킴
[CACHE, NOCACHE] -- CACHE는 메모리 상에서 시퀀스 값 관리 기본값은 20
```

<br>

### 시퀀스 수정 구문
- START WITH값은 변경이 불가능 합니다 삭제 후 다시 생성해야 합니다.
```sql
ALTER SEQUENCE 시퀀스명
[INCREMENT BY 증가숫자]
[MAXVALUE 최대숫자]
[MINVALUE 최소숫자]
[CYCLE, NOCYCLE]
[CACHE, NOCACHE]
```

<br>

### NEXTVAL, CURRCAL
- NEXTVAL : 시퀀스 다음 값
- CURRCAL : 시퀀스 현재 값
> SELECT문, INSERT문의 SELECT절, VALUE절, SET절에 사용 가능 합니다
```sql
시퀀스명.NEXTVAL
```