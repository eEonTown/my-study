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

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;

// 객체를 받기위한 ArrayList선언
ArrayList<TEST> list = new ArrayList<>();

// jdbc과정에 필요한 객체 선언
Connection conn = null; // DB연결
Statement stmt = null;  // Connection으로 sql구문 실행
ResultSet rset = null;  // sql실행 후 결과 저장

// 실행시킬 sql문을 문자열에 담아 놓음
String sql = "SELECT NUM, NAME FROM TEST";
```

<br>

- 예외처리를 해야 해서 try블럭 내에 작성 합니다.
- Statement의 명령결과를 받을 때 select문일 경우 executeQuery, DML문일 경우 executeUpdate(행 수 반환)를 사용합니다.
- executeUpdate는 숫자를 반환하기 때문에 ResultSet대신 int형 변수에 보관합니다.
```java
// 드라이버를 메모리에 등록
Class.forName("oracle.jdbc.driver.OracleDriver");

// Connection객체 생성 DB연결 => DriverManager.getConnection(url, id, pw)
conn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:xe", "jdbc", "jdbc");

// Connection에서 구문을 실행해줄 Statement객체 생성
stmt = conn.createStatement();

// statement실행 결과를 ResultSet으로 받아 사용
rset = stmt.executeQuery(sql);

// 데이터 전체를 조회한다면 while문을 사용합니다.
while(rset.next()){
    list.add(new Test(rset.getInt("NUM"), rset.getString("NAME"))); // 매개변수 생성자로 객체 생성
}
```

<br>

- finally문에서 실행순서 역순으로 자원을 반납합니다.
```java
finally {
	try {
		rset.close();
		stmt.close();
		conn.close();
	} catch (SQLException e) {
		e.printStackTrace();
	}
}
```

<br>

### 전체 코드
```java
public static void main(String[] args){

    ArrayList<Test> list = new ArrayList<>();
		
    Connection conn = null;
	Statement stmt = null;
	ResultSet rset = null;
		
	String sql = "SELECT NUM, NAME FROM TEST";
		
	try {
		Class.forName("oracle.jdbc.driver.OracleDriver");
		conn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:xe", JDBC, JDBC);
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