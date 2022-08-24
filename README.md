# 정보처리산업기사 공개용문제풀이

![image](https://user-images.githubusercontent.com/102296551/186313893-38494e17-6fb4-4c50-a08b-5c91744e352a.png)

공개된 문제 내용에따라 파일을 만들었습니다.

#index.jsp

![image](https://user-images.githubusercontent.com/102296551/186314414-a4bd1b99-8a36-4be3-9524-f3e442f618cc.png)

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>index</title>
<link rel="stylesheet" href="css/style.css">
</head>          
<body>
<header id="header">
<jsp:include page="layout/header.jsp"></jsp:include>
</header>
<nav id="nav">
<jsp:include page="layout/nav.jsp"></jsp:include>
</nav>
<section class="section">
<jsp:include page="layout/section.jsp"></jsp:include>
</section>
<footer id=footer>
<jsp:include page="layout/footer.jsp"></jsp:include>
</footer>
</body>  
</html>
```
화면에서 다른 정보들을 볼 수 있게 header, nav, section, footer을 넣었습니다.

# header.jsp

![image](https://user-images.githubusercontent.com/102296551/186315690-80bbeb50-e385-4da3-9567-13586297492d.png)

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>header</title>
<link rel="stylesheet" href="../css/style.css">
</head>
<body>
<header id="header">
<h1>쇼핑몰 회원관리 ver 1.0</h1>
</header>
</body>
</html>
```
header는 화면 맨 위에 보이기때문에 제목을 보여주는 코드를 짰다.

# nav.jsp

![image](https://user-images.githubusercontent.com/102296551/186316802-9ad3cff5-2466-475b-85ba-301b4b6574de.png)

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>nav</title>
<link rel="stylesheet" href="../css/style.css">
</head>
<body>
<nav id="nav">
<ul>
	<li><a href="join.jsp">회원등록</a></li>
	<li><a href="#">회원목록조회/수정</a></li>
	<li><a href="#">회원매출조회</a></li>
	<li><a href="index.jsp">홈으로</a></li>
</ul>
</nav>
</body>
</html>
```
nav페이지는 navigation페이지이므로 다른 페이지로 갈 수 있는 경로들을 지정해주었습니다.(링크)

# section.jsp

![image](https://user-images.githubusercontent.com/102296551/186317470-a0a9fa5a-57cb-4c08-9e74-6d1364f8d726.png)

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>section</title>
<link rel="stylesheet" href="../css/style.css">
</head>
<body>
<section class="section">
<h2>쇼핑몰 회원관리 프로그램</h2>
<p>
쇼핑몰 회원정보와 회원매출정보 데이터베이스를 구축하고 회원관리 프로그램을 작성하는 프로그램이다.<br>
프로그램 작성 순서<br>
1. 회원정보 테이블을 생성한다.<br>
2. 매출정보 테이블을 생성한다.<br>
3. 회원정보, 매출정보 테이블에 제시된 문제지의 참조데이터를 추가 생성한다.<br>
4. 회원정보 입력 화면프로그램을 작성한다.<br>
5. 회원정보 조회 프로그램을 작성한다.<br>
6. 회원매출정보 조회 프로그램을 작성한다.<br>
</p>
</section>
</body>
</html>
```

그냥메인화면의 섹션부분을 만들었기때문에 글자만 작성하였다.

# footer.jsp

![image](https://user-images.githubusercontent.com/102296551/186318142-39a8993d-98f6-4587-a312-4610d8dea304.png)

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>footer</title>
<link rel="stylesheet" href="../css/style.css">
</head>
<body>
<footer id="footer">
<p>
HRDKOREA Copyrighi@2022 All rights reserved, Human Resources Development Service of Korea.
</p>
</footer>
</body>
</html>
```

요것도 문제에선 화면하단에 저작권만 표시되어있기에 글자만 적는 코드를 썼다.

# join.jsp

```jsp
<%@ page import="DB.DBConnect"%>
<%@ page import="java.sql.*"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	String sql="select max(custno) from member_tbl_02";

	Connection conn = DBConnect.getConnection(); //DataBase와 연결
	PreparedStatement pstmt = conn.prepareStatement(sql);
	ResultSet rs = pstmt.executeQuery(); //Query문을 실행시키고 마지막 번호를 입력받는다. 그리고 rs에 저장.
	
	rs.next();
	int num = rs.getInt(1)+1; //rs에 1을 더함
%>  
```

join페이지에서 입력받은 값들을 DB로 옮겨 실행시키기 위한 코드로, 코드를 실행시키기 위해서 java.sql.*을 import 시켜줬고,
페이지와 DB를 연결시켜주기 위한 클래스 DBConnect도 import 시켜주었다.


```JavaScript
<script type="text/javascript">
	function checkValue() {
		if(!document.data.custname.value) {
			alert("회원성명을 입력하세요."); //value가 비어있으면 alert창을 띄움.
			data.custname.focus();  
			return false;
		} 
		else if(!document.data.phone.value) {
			alert("전화번호를 입력하세요."); //value가 비어있으면 alert창을 띄움.
			data.phone.focus();
			return false;
		} 
		else if (!document.data.address.value) {
			alert("주소를 입력하세요."); //value가 비어있으면 alert창을 띄움.
			data.address.focus();
			return false;
		} 
		else if (!document.data.joindate.value) {
			alert("가입일자를 입력하세요."); //value가 비어있으면 alert창을 띄움.
			data.joindate.focus();
			return false;
		} 
		else if (!document.data.grade.value) {
			alert("고객등급을 입력하세요."); //value가 비어있으면 alert창을 띄움.
			data.grade.focus();
			return false;
		}  
		else if (!document.data.city.value) {
			alert("도시코드를 입력하세요."); //value가 비어있으면 alert창을 띄움.
			data.city.focus();
			return false;
		}
		return true;
	}
</script>
```
JS로 checkValue라는 function을 만듬. 


```jsp
<section class="section">
   	 <h2>홈쇼핑 회원 등록</h2><br>

<form name="data" action="join_p.jsp" method="post" onsubmit="return checkValue()">
			<table class="table_line"> //class가 table_line인 table을 생성.
				<tr>
					<th>회원번호(자동발생)</th>
					<td><input type="text" name="custno" value="<%= num %>"  readonly ></td> //na
				</tr>
				<tr>
					<th>회원성명</th>
					<td><input type="text" name="custname" ></td>  //input의 name이 js에서 data.XXXX.focus값이 같아야됨
				</tr>
				<tr>
					<th>회원전화</th>
					<td><input type="text" name="phone" ></td>
				</tr>
				<tr>
					<th>회원주소</th>
					<td><input type="text" name="address" ></td>
				</tr>
				<tr>
					<th>가입일자</th>
					<td><input type="text" name="joindate" ></td>
				</tr>
				<tr>
					<th>고객등급[A:VIP,B:일반,C:직원]</th>
					<td><input type="text" name="grade" ></td>
				</tr>
				<tr>
					<th>도시코드</th>
					<td><input type="text" name="city" ></td>
				</tr>
				<tr class="center">
					<td  colspan="2" >
						<input type="submit" value="등록"> submit타입으로 받기때문에 
						<input type="button" value="취소" onclick="location.href='join.jsp'"> //onclick 이벤트를 받아서 실행시킴
						<input type="button" value="조회" onclick="location.href='member_list.jsp'"> //onclick 이벤트를 받아서 실행시킴
				</tr>
			</table>
		</form>	
   	
 </section>
 ```
 
 table을 만들고, type이 text인 input을 만듬. (name이 data.XXX.focus랑 같아야함.)
 
 


