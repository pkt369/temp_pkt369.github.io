---

layout : posts

title : "자바 Database연동2"

date : 2020-07-19

categoris : Java

---

먼저 새로운 class를 만드는데 이름은 보통 원하는이름DAO(MovieDAO)라고 짓습니다.

코드를 보면서 설명을 하겠습니다.

```java
public class MovieDAO {
	BasicDataSource ds;

	private String driver = "oracle.jdbc.driver.OracleDriver";
	private String url = "jdbc:oracle:thin:@localhost:1521:xe";
	private String userid = "scott"; //자신이 사용한 아이디
	private String passwd = "tiger"; //데이터베이스의 비밀번호

	public MovieDAO(){
		ds = new BasicDataSource(); //Connection Pool 기능과 Thread-safe 기능을 갖춤.
		ds.setDriverClassName(driver);
		ds.setUrl(url);
		ds.setUsername(userid);
		ds.setPassword(passwd);

		ds.setInitialSize(5);
	}
```

코드를 보시면 조금 생소한 코드들이 보이실겁니다. 많이 사용하시면서 데이터베이스와 많이 친해지시길 바랍니다.

`userid`는 데이터베이스의 ID, `passwd`는 암호이고,
접속할 DB의 url은 [jdbc] : [DBMS이름] @ [주소] : [포트] : [데이터베이스 식별자] 입니다.
driver는 ojdbc6.jar에 있는 OracleDriver를 로딩하는 것입니다.

그다음은 `Insert`, `delete`, `select` 를 통해 데이터를 주고받고할 것입니다.

다음은 메소드입니다.

```java
public void insertMovie(String name, int num, String url) {
		Connection conn = null;
		String sql = "insert into movies values(?, ?, ?)";
		PreparedStatement pstmt = null;
		try {
			conn = ds.getConnection();
			pstmt = conn.prepareStatement(sql);
			pstmt.setString(1, name);
			pstmt.setInt(2, num);
			pstmt.setString(3, url);

			int result = pstmt.executeUpdate();

			if(result == 1) {
				System.out.println("성공");
			}else {
				System.out.println("실패");
			}
		} catch (SQLException e) {			
			e.printStackTrace();
		}
	}
```

제가 하고있는 개인프로젝트에서 가져온 코드입니다.

`insert-이름` 이름을 이렇게 지었고, 매개변수로는 테이블이 가지고 있는 변수들의 값입니다.

`conn`은 null값으로 초기화시켜준 뒤 연결해서 사용하는 코드입니다.

sql 문은 데이터베이스언어로 3개의 매개변수를 안에다가 넣어주는 방식입니다.

<hr>

```java
public ArrayList<Movie> selectMovie() {
		Connection conn = null;
		PreparedStatement pstmt = null;
		String sql = "select * from movies";
		ArrayList<Movie> list = new ArrayList<Movie>();
		ResultSet rs = null;

		try {
			conn = ds.getConnection();
			pstmt = conn.prepareStatement(sql);
			rs = pstmt.executeQuery();

			while(rs.next()) {
				Movie mov = new Movie();

				mov.setName(rs.getString("name"));
				mov.setAge(rs.getInt("age"));
				mov.setUrl(rs.getURL("url"));

				list.add(mov);
			}

			return list;
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return null;
	}
```

`select문`은 전체데이터를 가져오는 것입니다.

ArrayList를 만든 뒤에 데이터를 `while(rs.next()){}` 을통해서 데이터를 list에 하나씩 넣어주는 방식입니다.

<hr>

```java
public void deleteMovie(String name) {
		//영화이름이 있는지 확인
		ArrayList<Movie> list = selectMovie();
		int count = 0;
		for(Movie e : list) {
			if(e.getName().equals(name)) {
				count++;
				break;
			}
		}
		if(count == 0) {
			return;
		}
		Connection conn = null;
		PreparedStatement pstmt = null;
		String sql = "delete from movies where name = ?";

		try {
			conn = ds.getConnection();
			pstmt = conn.prepareStatement(sql);
			pstmt.setString(1, name);

			pstmt.executeUpdate();


		} catch (SQLException e) {
			e.printStackTrace();
		}

	}
```

delete는 말그대로 삭제에 관련된 메소드입니다.

ArrayList를 생성해서 위의 메소드인 select문을 통해서 가져와서 저장을 먼저하고, 그다음 포문을 통해서 매개변수로 받은 이름이 없나 확인 하는 것입니다. 없다면 메소드를 `return`을 통해서 벗어나게 됩니다.

그리고 `executeUpdate`를 통해 데이터베이스에서 삭제하게 됩니다.
