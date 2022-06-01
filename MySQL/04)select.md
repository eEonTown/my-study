# SELECT
>테이블에서 데이터를 조회 합니다.
>
## 조회
```
SELECT 칼럼1, 칼럼2, ... FROM 테이블명;
//[LIMIT 옵셋, 조회할 행 수]
//[WHERE 대상칼럼=칼럼값]
//[AND]
//[OR]
//대괄호의 값은 테이블명 구문 이후 생략가능 합니다.
```
```
SELECT * FROM animals;
//*은 animals테이블의 모든 데이터를 조회 합니다.

SELECT name FROM animals;
//animals테이블의 name칼럼 데이터를 조회 합니다.

SELECT * FROM animals WHERE numbers=3;
//animals테이블의 number칼럼에서 3의 데이터를 가진 값 모두를 조회 합니다.

SELECT * FROM animals WHERE gender='수컷' OR legs=4;
//animals테이블의 gender칼럼에서 데이터가 수컷인 데이터와 leg칼럼에서 데이터가 4인 데이터를 조회 합니다.

SELECT * FROM animals WHERE gender='수컷' AND legs=4;
//animals테이블의 gender칼럼에서 데이터가 수컷인 이면서 leg칼럼에서 데이터가 4인 데이터를 조회 합니다.

SELECT * FROM animals LIMIT 1;
//animals테이블의 행 1개의 데이터를 가져옵니다.

SELECT * FROM animals LIMIT 1, 3;
//animals테이블의 1번째 행부터 행 3개의 데이터를 가져옵니다.
//순서가 0번째부터 시작한다는 것을 숙지해야 합니다.
```
엄청난 양의 데이터를 조회한다고 가정했을 때 `SELECT * FROM 테이블명`만 사용 한다면 모든 데이터를 불러오게 되어   
문제가 생길 수 있습니다.   
데이터가 많다면 꼭 `LIMIT`와`WHERE`을 이용해서 조회 해야 합니다.   

<br/>

# 그룹핑
>특정한 칼럼을 기준으로 해서 데이터를 그룹화 합니다.

## GROUP BY
```
SELECT * FROM 테이블명 GROUP BY 그룹할칼럼명;
```
```
SELECT gender animals GROUP BY gender;
//animals테이블의 gender의 데이터 암컷, 수컷을 그룹핑 합니다.
```

<br/>

# 정렬
>지정된 칼럼을 기준으로 행을 정렬합니다.

## ORDER BY
```
SELECT * FROM 테이블명 ORDER BY 정렬할칼럼명;
[DESC]
[ASC]
//대괄호의 값은 정렬할칼럼명 구문 이후 생략가능 합니다.
```
```
SELECT * FROM animals ORDER BY number;
SELECT * FROM animals ORDER BY number ASC;
//animals테이블의 number을 오름차순으로 정렬 합니다.

SELECT * FROM animals ORDER BY number DESC;
//animals테이블의 number을 내림차순으로 정렬 합니다.

SELECT * FROM animals ORDER BY number ASC, name DESC;
//animals테이블의 number을 오름차순으로 정렬 후 고정된 상태에서 name을 다시 정렬 합니다.
```

<br/>

# INDEX
>데이터를 조회할 때 원하는 데이터를 빠르게 찾을 수 있게 만드는 데이터 입니다.
- 자주 조회하는 칼럼에 적용합니다.
- 데이터 조회시 오랜시간이 걸리는 칼럼에 적용합니다.
- 게시판의 글이나 URL처럼 데이터가 긴 경우에는 사용하지 않습니다.

## 인덱스의 종류
>key는 table작성 시 칼럼작성 구문 다음부터 작성합니다.
>데이터가 중복되는걸 방지 할 땐 primary와 unique를 사용합니다.

### primary key
>테이블의 number와 같은 하나밖에 없는 값이 지정 되어야 합니다.
- 테이블마다 하나의 primary key를 가질 수 있습니다.
- 테이블 내의 중복되지 않는 데이터값을 지정해야 합니다.
- WHERE문으로 데이터를 조회 시 가장 빠르게 데이터를 가져 옵니다.
```
PRIMARY KEY(지정칼럼)
```

### unique key
>primary key와 같습니다만 primary key는 오직 하나만 설정이 가능하다면 unique key는 칼럼마다 지정이 가능합니다.
- 여러개의 unique key를 지정 할 수 있습니다.
- 테이블 내의 중복되지 않는 데이터값을 지정해야 합니다.
- primary key와 같이 빠르게 데이터를 조회하지만 경우에 따라서는 primary key보다 느립니다.
```
UNIQUE KEY 키이름 (지정칼럼)
//키이름을 생략하면 자동으로 키이름을 생성 합니다.
```

### normal key
- 중복이 가능합니다.
- primary, unique보다 속도가 느립니다.
- 여러개의 normal key를 지정 할 수 있습니다.
```
KEY 키이름 (지정칼럼)
KEY 키이름 (지정칼럼, 지정칼럼)
//key를 여러번 정의 할 수 있습니다.
```
두번째 구문처럼 하나의 KEY안에 두개의 칼럼을 지정한 것을 `중복키` 라고 합니다.   
예를 들어 이름, 주소 칼럼이 있는데, 이름과 주소를 같이 검색하는 경우가 있을 때   
KEY에 칼럼을 묶어 중복키를 작성합니다.