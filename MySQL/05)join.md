# 테이블 분할
>데이터의 양이 많아지면 하나의 테이블에 모든 데이터를 수용하는게 어렵고 비효율적입니다.   
>그래서 테이블을 분할해서 서로 관계성을 부여해 관리하면 효율적입니다.   

만약 칼럼내에 동일한 데이터가 존재한다고 가정했을 때 그 칼럼을 묶어서 테이블을 따로 만들어 관리한다면 모든 방면에서 효율적일 것입니다.

<br/>

## JOIN
>분할된 테이블을 하나의 테이블인 것처럼 결과를 출력합니다.   
>JOIN의 종류에는 두가지가 있습니다
* **OUTER JOIN**
    + LEFT JOIN (가장 많이 사용되는 형태)
    + RIGHT JOIN
* **INNER JOIN**

### OUTER JOIN
>분할된 테이블간에 매칭이 되는 행이 없으면 결과를 `NULL`로 표시하고 가져옵니다.

#### LEFT JOIN
>구문 왼쪽의 테이블을 기준으로 구문 오른쪽 테이블의 데이터를 가져옵니다.
```
//animals 테이블 생성
CREATE TABLE animals (
    number tinyint NOT NULL,
    name varchar(10) NOT NULL,
    gender enum('암컷', '수컷') NOT NULL,
    size_id tinyint NOT NULL,
    PRIMARY KEY(number)
);

//size 테이블 생성
CREATE TABLE size (
    number tinyint NOT NULL,
    size varchar(10) NOT NULL,
    weight int NOT NULL,
    PRIMARY KEY(number)
);
```
![image](https://user-images.githubusercontent.com/102468071/161428958-20e66fd6-86dd-40d1-bae4-d1c3690bfad2.png)

테이블 생성 후 데이터를 넣었다고 가정 했을 때 가장 많이 사용하는 조인의 형태인 LEFT JOIN으로 결과를 보겠습니다.
```
SELECT a.name, a.size_id, s.size, s.weight FROM animals AS a LEFT JOIN size AS s ON a.size_id = s.number;
```
![image](https://user-images.githubusercontent.com/102468071/161428974-d6a4493a-e6ad-4387-aa20-4acee0041034.png)
![image](https://user-images.githubusercontent.com/102468071/161429278-3383360a-0046-4a22-8ec7-2087b98ebc89.png)







### INNER JOIN
>분할된 테이블간에 두 테이블 모두 데이터가 존재하는 행만 결과를 가져옵니다.