# DDL
- 객체를 CREATE, ALTER, DROP하는 구문 입니다.

<br>

### CREATE
- 테이블이나 인덱스, 뷰 등 객체를 생성하는 구문 입니다
```sql
CREATE TABLE 테이블명
(
    컬럼명 자료형(크기),
    컬럼명 자료형(크기),
    ...
);
```

<br>

### 컬럼 주석
- 테이블 생성 후 컬럼에 주석을 남깁니다.
```sql
COMMENT ON COLUMN 테이블명.컬럼명 IS '주석';
```

<br>
<br>

# 제약조건

<br>

### PRIMARY KEY(PK / 기본키)
- 테이블당 하나만 가질 수 있는 키로 해당 키를 가진 컬럼의 데이터는 중복이 불가능합니다.
- NULL값도 올 수 없습니다.
- 컬럼 2개를 묶어 하나의 PRIMARY KEY에 지정은 가능 합니다.
```sql
CREATE TABLE 테이블명
(
    컬럼명 자료형 [CONSTRAINT 제약조건명] PRIMARY KEY
);

CREATE TABLE 테이블명
(
    컬럼명 자료형,
    [CONSTRAINT 제약조건명] PRIMARY KEY(컬럼명)
);
```

<br>

### UNIQUE(고유키)
- RIMARY KEY와 비슷하게 중복 데이터를 값으로 가질 수 없습니다.
- 차이점은 NULL을 허용, 다수의 UNIQUE도 혀용합니다.
```sql
CREATE TABLE 테이블명
(
    컬럼명 자료형 [CONSTRAINT 제약조건명] UNIQUE
);

CREATE TABLE 테이블명
(
    컬럼명 자료형,
    [CONSTRAINT 제약조건명] UNIQUE(컬럼명)
);
```

<br>

### FOREIGN KEY(FK / 외래키)
- 다른 테이블을 참조 할 때 사용하며 컬럼을 지정하여 다른 테이블의 컬럼과 연동이 가능합니다.
> 연동 시 참조테이블은 부모테이블이 되며 부모 / 자식 관계가 생성 됩니다.
> 참조해야하는 테이블의 컬럼은 기본키, 고유키로 지정되어 있어야 합니다.
```sql
CREATE TABLE 테이블명
(
    컬럼명 자료형 [CONSTRAINT 제약조건명] REFERENCES 참조할테이블명(참조할컬럼명)
);

CREATE TABLE 테이블명
(
    컬럼명 자료형,
    [CONSTRAINT 제약조건명] FOREIGN KEY(컬럼명) REFERENCES 참조할테이블명(참조할컬럼명)
);
```

<br>

##### 부모 컬럼 삭제
> 자식 테이블에서 부모 테이블을 참조 중이기 때문에 삭제가 불가능합니다.
> 삭제하고 싶다면 자식의 컬럼값을 삭제 후 부모 컬럼 값을 삭제해야 합니다.

##### 다른 삭제 방법
- 테이블을 생성 할 때 제약조건에 조건을 붙여주면 삭제가 간편합니다
- ON DELETE CASCADE : 부모테이블의 값을 삭제하면 자식 테이블의 값도 삭제됨
- ON DELETE SET NULL : 부모테이블의 값을 삭제하면 자식 테이블의 값은 NULL로 바뀜
```sql
CREATE TABLE 테이블명
(
    컬럼명 자료형 [CONSTRAINT 제약조건명] REFERENCES 참조테이블명(참조컬럼명) [조건]
);
```

<br>

### CHECK
- 입력되는 값이 지정한 조건에 맞지 않으면 오류를 반환합니다.
```sql
CREATE TABLE 테이블명
(
    컬럼명 자료형 [CONSTRAINT 제약조건명] CHECK(조건식)
);

CREATE TABLE 테이블명
(
    컬럼명 자료형,
    [CONSTRAINT 제약조건명] CHECK(조건식)
);
```

<br>

### NOT NULL
- 컬럼에 NULL값과 공백을 허용 하지 않음을 의미합니다.
```sql
CREATE TABLE 테이블명
(
    컬럼명 자료형 [CONSTRAINT 제약조건명] NOT NULL
);
```