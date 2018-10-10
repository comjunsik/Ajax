# index.jsp
검색란과 검색버튼에 이벤트 달아주기
```jsp
<div class="col-xs-8">
	<input class="form-control" id="userName" onkeyup="searchFunction()"  type="text" size="20">
</div>
<div class="col-xs-2">
	<button class="btn btn-primary" onclick="searchFunction();" type="button">검색</button>
</div>
```
**id="userName" onkeyup="searchFunction()"**<br>
id를 입력해 준후 onkeyup에 함수이름
onkeyup은 키보드 이벤트, 사용자가 키를 실행할때(타자를 칠때)에 스크립트를 실행
즉, 키보드를 칠때마다 searchFunction()이 실행됨.

**onclick="searchFunction();"**<br>
버튼에 onclick을 달아줌으로써 버튼 클릭시 searchFunction()이 실행되게 한다.

```jsp
<table class="table" style="text-align: center; border: 1px solid #dddddd">
	<thead>
		<tr>
			<th style="background-color: #fafafa; text-align: center;">이름</th>
			<th style="background-color: #fafafa; text-align: center;">나이</th>
			<th style="background-color: #fafafa; text-align: center;">성별</th>
			<th style="background-color: #fafafa; text-align: center;">이메일</th>
		</tr>
	</thead>
	<tbody id="ajaxTable"></tbody>
</table>
```
&lt;tbody>에 id 값을 줌으로써 javascript로 처리할 수있도록 한다.

```jsp
<script type="text/javascript">
	var searchRequest = new XMLHttpRequest();
	var registerRequest = new XMLHttpRequest();
	function searchFunction(){
			searchRequest.open("Post", "./UserSearchServlet?userName=" + encodeURIComponent(document.getElementById("userName").value), true);
			searchRequest.onreadystatechange = searchProcess;
			searchRequest.send(null);
			
	}
	
	function searchProcess({
			var table = document.getElementById("ajaxTable");
			table.innerHTML = "";
			if(searchRequest.readyState == 4 && searchRequest.status == 200){
				var object = eval('(' + searchRequest.responseText + ')');
				var result = object.result;
				for(var i = 0; i < result.length; i++) {
					var row = table.insertRow(0);
					for(var j = 0; j < result[i].length; j++){
						var cell = row.insertCell(j);
						cell.innerHTML = result[i][j].value;
				}
			}
		}
	}
		
	window.onload = function(){
			searchFunction();
	}
		
	</script>
```
>**var searchRequest = new XMLHttpRequest();**<br>
JavaScript를 이용하여 서버로 보내는 HTTP request를 만들기 위해서는 그에 맞는 기능을 제공하는 Object의 인스턴스가 필요합니다. XMLHttpRequest 가 그러한 Object의 한 예입니다. 이러한 로직은 Internet Explorer의 XMLHTTP 라고 불리는 ActiveX 객체로 부터 시작되었습니다.

```jsp
function searchFunction(){
	searchRequest.open("Post", "./UserSearchServlet?userName=" + encodeURIComponent(document.getElementById("userName").value), true);
	searchRequest.onreadystatechange = searchProcess;
	searchRequest.send(null);
			
		}
```

XHTTPrequest 객체의open()과 send()를 통해 요청을 할 수 있다.
>open()메소드의 파라미터
 <li>첫번째 파라미터는 HTTP 요구 방식(request method) ─ GET, POST, HEAD 중의 하나이거나 당신의 서버에서 지원하는 다른 방식 ─ 입니다. 이 파라미터는 HTTP 표준에 따라 모두 대문자로 표기해야합니다. 그렇지 않으면 (파이어폭스와 같은) 특정 브라우저는 이 요구를 처리하지 않을 수도 있습니다.

 <li>두번째 파라미터는 요구하고자하는 URL 입니다. 보안상의 이유로 서드 파티 도메인 상의 URL은 기본적으로 호출할 수 없습니다. 요구하는 모든 페이지에 정확한 도메인 네임을 사용하십시오. 그렇지 않으면 open() 메소드를 호출할 때 'permission denied' 에러가 발생할 수 있습니다. 일반적인 오류는 당신의 사이트에 domain.tld 와 같은 형태로 접근하는 것 입니다. 이러한 경우 www.domain.tld 와 같은 형태로 페이지를 요구하기 바랍니다. 

 <li>세번째 파라미터(생략 가능)는 요구가 비동기식(Asynchronous)으로 수행될 지를 결정합니다. 만약 이 파라미터가 true(기본값) 으로 설정된 경우에는 자바스크립트 함수가 지속적으로 수행될 수 있어 서버로부터 응답을 받기 전에도 유저와 페이지의 상호작용이 계속 진행됩니다. 이것이 AJAX 의 첫번째 A (Asynchronous : 비동기성) 입니다.
false로 설정된 경우 동기적으로 작동합니다. (send() 함수에서 서버로부터 응답이 올 때까지 기다림)

![xmlhttpreqeust 1](https://user-images.githubusercontent.com/41488792/46736005-d5627c80-ccd2-11e8-9121-9b5c2ba12717.PNG)

![xmlhttpreqeust 2](https://user-images.githubusercontent.com/41488792/46736016-df847b00-ccd2-11e8-849a-1467bb0e63e4.PNG)

출처:https://developer.mozilla.org/ko/docs/Web/Guide/AJAX/Getting_Started

```jsp
searchRequest.open("Post", "./UserSearchServlet?userName=" + encodeURIComponent(document.getElementById("userName").value), true);
```
>**encodeURIComponent(encodedURIString)**<br>
텍스트 문자열을 유효한 URI(Uniform Resource Identifier) 구성 요소로 인코딩합니다.
**document.getElementById("userName").value**<br>
form에 있는 데이터의 유효성을 체크하기 위해, 우리는 웹 페이지로부터 데이터를 잡아낼 필요가 있다. 자바 스크립트가 포함된 웹 페잊 엘리멘트(Element)에 접근하기 위한 핵심 열쇠가 HTML 태그의 id 속성이다.
document.getElementById().value는
해당하는 엘리멘트의 ID를 가져오는 함수이다.
