# Table
>데이터가 저장되는 장소

## schema
>테이블에 저장될 데이터의 구조와 형식을 정의 하는 것

## 테이블 생성
```
CREATE TLE 테이블명 (
    칼럼명 데이터타입,
    칼럼명 데이터타입
)
```
```
CREATE TABLE animals (
    number tinyint NOT NULL,
    name char(10) NOT NULL,
    gender enum('암컷', '수컷') NOT NULL,
    legs tinyint(4) NOT NULL,
    primary key (number)
);
```
NOT NULL은 값이 반드시 들어와야 한다는 의미 입니다.       
primary key는 NULL 값을 가질 수 없으며, 또한 중복된 값을 가질 수 없습니다.

## 테이블 리스트 확인
```
SHOW TABLES;
```

## 테이블 스키마 열람
```
desc 테이블명;
```

## 테이블 제거
```
DROP TABLE 테이블명;
```