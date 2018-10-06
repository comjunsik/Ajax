# Ajax-1
Ajax연습 기초

![ajax 1](https://user-images.githubusercontent.com/41488792/46566805-8d54fa00-c960-11e8-8fc3-831ecdb932d3.PNG)

![default](https://user-images.githubusercontent.com/41488792/46566812-ab225f00-c960-11e8-93ce-ee4f4fcaa452.PNG)

![ajax 2](https://user-images.githubusercontent.com/41488792/46566819-c7be9700-c960-11e8-959a-4ffe585b7b3d.PNG)

![ajax](https://user-images.githubusercontent.com/41488792/46566821-df961b00-c960-11e8-887e-86cf47765c5f.PNG)

[출처:https://coding-factory.tistory.com/143]

---
# index.jsp

```jsp
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="css/bootstrap.css">
	<title>Insert title here</title>
	<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
	<script src="js/bootstrap.js"></script>
</head>
```
>**viewport란 무엇일까?**<br>
viewport란 우리말로 의 뷰포트와 모바일보임창, 즉 화면 상의 화상 표시 영역을 뜻합니다.
데스크탑(pc)의 뷰포트와 모바일 뷰포트는 약간 다릅니다.

>**viewprot 크기 조절이 필요한 이유?**<br>
데스크탑에 기반하여 설계된 웹페이지를 모바일에서 보면 기본 뷰포트가 980px이기 때문에 내용이 작게 보입니다.
뷰포트 설정을 하게 되면 다양한 모바일 기기에서도 페이지의 너비나 화면 배율을 설정할 수 있습니다.
모바일 장치에 최적화된 웹페이지를 만들려면 html 문서 head에 뷰포트 설정을 포함해야 합니다.
![viewport](https://user-images.githubusercontent.com/41488792/46566982-2df8e900-c964-11e8-912a-a600bd0702d5.PNG)

출처:http://aboooks.tistory.com/352

반응형 웹에 사용되는 meta 태그를 넣어주자 (bootstrap 사용)<br>
 **width** 속성은 뷰포트의 크기를 조정한다. 특정한 숫자를 사용해 width=600이라고 할 수도 있고 devie-width와 같은 특정한 값을 사용할수 있는데, <strong>device-width</strong>는 100% 스케일에서 CSS 픽셀들로 계산된 화면의 폭을 의미한다.<br>
  **initial-scale** 속성은 페이지가 처음 로드될 때 줌 레벨을 조저한다.(사용자가 얼마나 페이지를 줌-인, 줌-아우트 할 수 있는지를 조정한다.<br>
 **rel="stylesheet"** 스타일 시트는 html이 가지는 불편함 점을 해소하기 위해서 만들어진 html의 보완 도구다.(CSS사용)<br>
 -->BBS-2 resporiry에 있음

 **&lt;script src="https://code.jquery.com/jquery-3.1.1.min.js">&lt;/script>**
외부 자바스크립트 라이브러리 추가

# UserDAO.java
회원 조회 함수
```java
public ArrayList<User> search(String userName){
		String SQL = "SELECT * FROM USER WHERE userName LIKE ?";
		ArrayList<User> userList = new ArrayList<User>();
		try {
			pstmt = conn.prepareStatement(SQL);
			pstmt.setString(1, userName);
			rs = pstmt.executeQuery();
			while(rs.next()) {
				User user = new User();
				user.setUserName(rs.getString(1));
				user.setUserAge(rs.getInt(2));
				user.setUserGender(rs.getString(3));
				user.setUserEmail(rs.getString(4));
				userList.add(user);
				
			}
			
		} catch (Exception e) {
			e.printStackTrace();
		}
		return userList;
	}
```
**public ArrayList&lt;User> search(String userName)**<br>
User클래스를 저장하는 ArrayList를 반환값으로
**String SQL = "SELECT * FROM USER WHERE userName LIKE ?";**<br>
```JAVA
pstmt = conn.prepareStatement(SQL);
pstmt.setString(1, userName);
```
SQL문 ?에 userName을 삽입
따라서 userName에 들어가는 문자열로 테이블 검색
