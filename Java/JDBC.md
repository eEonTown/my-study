# JAVA 자바 JDBC 오라클 DB 연동
- JDBC : 데이터베이스 시스템에 접근할 수 있는 자바 API입니다.

<br>

### 오라클 DB연동
- 자바 프로젝트와 데이터베이스를 연결하기 위해서는 오라클드라이버(ojdbc6.jar)를 BuildPath에 추가 시켜주어야 합니다.

> ojdbc6.jar경로 : C:\oraclexe\app\oracle\product\11.2.0\server\jdbc\lib
> 프로젝트에 추가 할 때 마다 매번 찾아가기 힘들기 때문에 파일을 복사해 따로 관리해주는것이 좋습니다.

<br>

### 코드 작성 순서
- DriverManager : Connection 객체를 생성하기 위한 객체 입니다.
- Connection : DB의 연결정보를 담고 있는 객체 입니다.
- Statement : 연결된 DB에 sql문을 전달해서 실행하고 그 결과를 받아내는 객체입니다.
- ResultSet : SELECT문의 결과를 저장하는 객체 입니다.
##### 1. DB연동을 위한 정보를 변수에 저장합니다.
```java
String driver = "oracle.jdbc.driver.OracleDriver";
String url = "jdbc:oracle:thin:@localhost:1521:xe";
String id = "JDBC";
String pw = "JDBC";

String sql = "SELECT NUM, NAME FROM TEST"; // SQL실행문 변수에 담아 놓음

ArrayList<Test> list = new ArrayList<>(); // 전체 조회 결과를 담을 자바 객체
```

<br>

##### 2. jdbc과정에 필요한 객체 선언
```java
Connection conn = null;
Statement stmt = null;
ResultSet = rset = null;
```

<br>

##### 3. 예외처리를 위해 try블럭 내에 작성
- 실행할 sql문이 select문일 경우 executeQuery => ResultSet 반환
- DML문일 경우 executeUpdate => int반환(행 수)
```java
try{
    Class.forName(driver); // jdbc 드라이버를 메모리에 등록
    conn = DriverManager.getConnection(url, id, pw); // Connection객체 생성 DB연결
    stmt = conn.createStatement(); // Connection에서 구문을 실행해줄 Statement객체 생성
    rset = stmt.executeQuery(sql); // Statement실행 결과를 ResultSet으로 받아서 사용

    while(rset.next()){ // 반복문을 이용해 ResultSet에 담겨있는 데이터를 자바 객체에 옮김
        list.add(new Test(rset.getInt("NUM"), rset.getString("NAME")));
    }

} catch (ClassNotFoundException e) {
	e.printStackTrace();
} catch (SQLException e) {
	e.printStackTrace();
} finally{/*4번 설명*/}
```

<br>

##### 4. finally블럭에서 객체 반납
- 사용한 jdbc용 객체를 생성된 역순으로 반납합니다.
```java
finally{
    try{
        rset.close();
        stmt.close();
        conn.close();
    } catch (SQLException e){
        e.printStackTrace();
    }
}
```

<br>

##### 5. 조회된 결과 출력
- 사용한 jdbc용 객체를 생성된 역순으로 반납합니다.
```java
if(list.isEmpty){
    System.out.println("조회 결과가 없습니다.");
} else{
    for(int i = 0; list.size(); i++){
        System.out.println(list.get(i));
    }
}
```

<br>

### select문 전체코드
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;

public static void main(String[] args){

ArrayList<Test> list = new ArrayList<>();
		
	String driver = "oracle.jdbc.driver.OracleDriver";
	String url = "jdbc:oracle:thin:@localhost:1521:xe";
	String id = "JDBC";
	String pw = "JDBC";
		
	Connection conn = null;
	Statement stmt = null;
	ResultSet rset = null;
		
	String sql = "SELECT NUM, NAME FROM TEST";
		
	try {
		Class.forName(driver);
		conn = DriverManager.getConnection(url, id, pw);
		stmt = conn.createStatement();
		rset = stmt.executeQuery(sql);
			
		while(rset.next()) {
			list.add(new Test(rset.getInt("NUM"), rset.getString("NAME")));
		}
	} catch (ClassNotFoundException e) {
		e.printStackTrace();
	} catch (SQLException e) {
		e.printStackTrace();
	} finally {
		try {
			rset.close();
			stmt.close();
			conn.close();
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
		
	if(list.isEmpty()) {
		System.out.println("조회결과가 없습니다.");
	}else {
		for(int i = 0; i < list.size(); i++) {
			System.out.println(list.get(i));
		}
	}
}
```

<br>

### DML문 전체코드
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public static void main(String[] args){
		
	String driver = "oracle.jdbc.driver.OracleDriver";
	String url = "jdbc:oracle:thin:@localhost:1521:xe";
	String id = "JDBC";
	String pw = "JDBC";
		
	Connection conn = null;
	Statement stmt = null;
	int result = 0;
		
	String sql = "INSERT INTO TEST VALUES (1, 'NAME')";
		
	try {
		Class.forName(driver);
		conn = DriverManager.getConnection(url, id, pw);
		stmt = conn.createStatement();
		result = stmt.executeUpdate(sql);
			
		if(result > 0){
			conn.commit(); // 데이터 추가 후 커밋
		} else{
			conn.rollback(); // 데이터 추가 실패 롤백
		}

	} catch (ClassNotFoundException e) {
		e.printStackTrace();
	} catch (SQLException e) {
		e.printStackTrace();
	} finally {
		try {
			stmt.close();
			conn.close();
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
		
	if(result > 0){
		System.out.println("등록 성공");
	} else{
		System.out.println("등록 실패");
	}
}
```