# Servlet이란?

![servlet 1](https://user-images.githubusercontent.com/41488792/46572233-24e83600-c9bd-11e8-9bc8-f72c14b604ba.PNG)

![servlet 2](https://user-images.githubusercontent.com/41488792/46572235-3598ac00-c9bd-11e8-89f5-58eb9ec171c1.PNG)

![servlet 3](https://user-images.githubusercontent.com/41488792/46572238-40ebd780-c9bd-11e8-8e96-37d68414e12b.PNG)

출처:http://mangkyu.tistory.com/14

![servlet 4](https://user-images.githubusercontent.com/41488792/46572324-cb810680-c9be-11e8-801c-d925e3d12188.PNG)

출처:http://jusungpark.tistory.com/15

----
# UserSearchServlet.java
```java
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("UTF-8");
		response.setContentType("text/html; charset-UTF-8");
		String userName=request.getParameter("userName");
	}
```
**doPost()**<br>
클라이언트 HTTP POST 요청에 대해 처리.
**request.setCharacterEncoding("UTF-8");**<br>
파라미터로 전달되는 데이터의 한글 처리(즉, 전송 받는 데이터를 한글로 받겠다.)
**userName=request.getParameter("userName");**<br>
브라우저로 보내지는 데이터의 한글 처리(즉, 서블릿을 통해 HTTP로 보낼 데이터를 한글로 처리하겠다.)

<h3>JSON 이란?<h3>
 2. 무엇을 줄인 말이냐?

    JavaScript Object Notation이라는 이름에서 알 수 있듯이 자바스크립트를 위한 것이고 객체 형식으로 자료를 표현하는 것이다.

    
  3. 이거 프로그래밍 언어냐?

    사방팔방에 JSON이라는게 등장하고 각종 사용방법이 나오고 어려워 보이지만 JSON 자체는 정말 별거 아니다. JSON 그자체 는 단순히 데이터 포맷일 뿐이다. 어떠한 통신 방법도, 프로그래밍 문법도 아닌 단순히 데이터를 표시하는 표현 방법일 뿐이다.
    간단한 데이터를 xml보다 좀 더 간단하게 표현하기 위해 만든 것이다. XML보다 기능이 적기 때문에 파싱도 빠르고 간단하기 때문에 클라이언트 사이드에서, 특히 모 바일에서 더욱 유용하겠다. 사실 서버 입장에서도 더 유용하기 때문에 많은 서비스들이 XML보다는 JSON을 권장한다.

    다시 말하지만 이건 프로그래밍 언어가 아니다.


  4. 이거 공식 사이트 없냐?

    네이버에서 JSON으로 검색하면 시덥잖은 네이버 자체 컨텐츠들(블로그, 카페, 지식인)만 뜨는데 JSON 공식 사이트는 멀쩡히 있고, 한국어도 지원된다.
      http://json.org/json-ko.html
    여기 들어가면 좀 당황스러울 수도 있다. 뭔 놈의 공식사이트가 내용이 진짜 간단하고 별 거 없기 때문이다.
    위키피디아를 보면 더 잘 설명이 되어 있다.
      http://ko.wikipedia.org/wiki/JSON


  5. 이거 왜 쓰냐?

    단순히 데이터를 받아서 객체나 변수로 할당해서 사용하기 위한 것이다.


  6. AJAX와는 다른가?

    AJAX와는 별개의 개념이지만 AJAX가 없다면 JSON이라는 개념은 필요 없을 것이다. AJAX를 사용해 데이터를 주고 받을 때 그 데이터 포맷으로 JSON을 사용하는 것이다.


  7. 이거 쓰려면 따로 라이브러리 같은 걸 써야 하냐?

    JSON 자 체는 이미 자바스크립트 표준으로 채택되어 자바스크립트에서 기본적으로 지원하고 있기 때문에 별도의 라이브러리가 필요하거나 하지는 않 다. 그냥 eval()이라는 함수 하나로 해결되는 게 JSON이다. 하지만 JSON의 한계로 인해 라이브러리를 따로 사용하는 경우가 많다.그리고 자바스크립트 이외의 환경에서도 JSON을 간단히 사용 하기 위한 라이브러리들이 존재한다. JSON 공식 사이트 내용의 대부분이 바로 그것이다.


  8. JSON 단점이나 문제점은 뭐냐?

    AJAX 는 단순히 데이터만이 아니라 javascript 그 자체도 전달할 수 있다. 무슨 말이냐면 json데이터라고 해서 받았는데 그게 단 순 데이터가 아니라 자바스크립트가 될 수도 있고, 그게 실행 될 수 있다는 것이다. 데이터인 줄 알고 받았는데 악성 스크립트더 라 뭐 그럴 수 있다는 것이다.
    JSON 관련 라이브러리를 따로 사용하는 이유가 이것이다. 받은 내용에서 순수하게 데이터만 추출하기 위한 라이브러리이다.


  9. JSON으로 아무 데이터나 불러갈 수 있냐?

    JSON의 한계는 JSON으로 가져올 수 있는 데이터는 해당 자바스크립트가 로드된 서버의 데이터에 한정된다는 것이다.
    예를 들어서 http://kwz.kr/json.js에서 불러올 수 있는 데이터는 kwz.kr 서버에 존재하는 것만 가능하다는 것이다. 구글 데이터를 불러온다거나 네이버 데이터를 불러온다거나 할 수 없다.
    JSON은 단순히 데이터 포맷일 뿐이고 그 데이터를 불러오기 위해선 XMLHttpRequest()라는 자바스크립트 함수를 사용해야 하는데 이 함수가 동일 서버에 대한 것만 지원하기 때문이다.


  10. 어? 다른 서버의 데이터도 가져가서 보여주던데??

    궁하면 통한다고 방법이야 만들면 나오는 거다. 그래서 나온 게 일종의 프락시 역할을 하는 서버쪽 스크립트 파일과 JSONP이다.


  11. JSONP는 뭐냐????

    JSON with Padding을 줄인 말이다. 다른 서버의 데이터를 가져오기 위한 방법이다.
    이건 해당 서버에서 JSONP의 방식을 지원해 줘야지만 가능하다. 이것이 불가능하면 역시 프락시를 써야 한다.

출처:http://egloos.zum.com/killins/v/3013974

AJAX를 사용할때 그 데이터 포맷을 JSON으로 한다.
getJSON()을 한다면 client가 요철을 보낼때 그 결과를 JSON형식으로 돌려 받겠다는 뜻이다.
이 JSON을 만들어내는 역할을 해당 Servlet이 하는 것이다.