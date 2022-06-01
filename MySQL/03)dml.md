# 삽입
>테이블에 데이터를 삽입 합니다.

```
INSERT INTO 테이블명 VALUES (값1, 값2, ...);

INSERT INTO 테이블명 (칼럼1, 칼럼2, ...) VALUES (값1, 값2, ...);
```
```
INSERT INTO animals VALUES ('1', 'tiger', '암컷', '4');

INSERT INTO animals (`number`, `name`, `gender`, `legs`) VALUES ('1', 'tiger', '암컷', '4');
```

<br/>

# 변경
>기존 테이블에 있는 데이터를 수정합니다.

```
UPDATE 테이블명 SET 칼럼1=칼럼1값, 칼럼2=칼럼2값 WHERE 대상칼럼=칼럼값;
```
![image](https://user-images.githubusercontent.com/102468071/160992306-586dbdbe-6da3-4138-a0de-1259ef5d303d.png)
```
UPDATE animals SET gender='암컷';
//animals테이블의 gender값을 모두 암컷으로 변경합니다.

UPDATE animals SET gender='암컷' WHERE name='dog';
//name에서 dog라는 값을 가진 gender를 암컷으로 변경합니다.
```
- 글자는 ''로 감싸주어야 하지만 숫자는 생략이 가능합니다.
- 테이블명, 칼럼명, 데이터베이스명을 지정 할 때 ``로 감싸주는 경우도 있는데 그 경우는 분명하게 구분을 하기위해 작성합니다.   
   예를 들어 SELECT는 SQL문법인데 테이블명이 select일 때 사용됩니다.   

<br/>

# 삭제
>행단위로 데이터를 삭제 합니다.

```
DELETE FROM 테이블명 WHERE 삭제하려는칼럼=값;
//WHERE은 생략 가능합니다.
```
```
DELETE FROM animals; //테이블의 데이터를 삭제 합니다.
DELETE FROM animals WHERE number=1; //number에서 1을 가진 데이터 행을 삭제합니다.
```

## TRUNCATE
>테이블 전체 데이터를 삭제 합니다.
>테이블에 외부키(foreign key)가 없으면 DELETE보다 빨리 삭제 됩니다.
>foreign key는 두 테이블을 서로 연결하는데 사용되는 키 입니다.

```
TRUNCATE 테이블명;
```

## DROP TABLE
>테이블 자체를 삭제 합니다.

```
DROP TABLE 테이블명;
```

- - -

## DROP, TRUNCATE, DELETE
>DROP, TRUNCATE, DELETE는 모두 삭제하는 구문입니다.

**DROP** : 데이터와 테이블 전체를 삭제합니다.   
**TRUNCATE** : 처음 테이블이 만들어졌던 상태로 돌아 갑니다. 테이블의 모든 데이터를 삭제하고 칼럼값만 남습니다.   
**DELETE** :  테이블의 데이터만 지워지고 데이터가 있던 공간은 남아있습니다.

![image](https://user-images.githubusercontent.com/102468071/160998119-444df9fa-4260-4f39-b09a-1c94f869f7ed.png)