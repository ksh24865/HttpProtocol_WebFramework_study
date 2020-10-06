# 1.HttpProtocol
## HTTP
* `HTTP(Hyper Text Transfer Protocol, 하이퍼텍스트 전송 방식)`이라는 규칙을 통하여 데이터를 주고 받기 위한 서버/클라이언트 모델을 따르는 프로토콜
* 하이퍼 텍스트는 하이퍼링크를 통하여 이곳에서 저곳으로 움직일 수 있는 텍스트라고 할 수 있다.
* #### 비연결성 ( Connectionless )
   * 클라이언트와 서버가 한 번 연결을 맺은 후, 클 라이언트 요청에 대해 서버가 응답을 마치면 맺었던 연결을 끊어 버리는 성질
   * 장점
      * 서버에서 다수의 클라이언트와 연결을 계속 유지해야 한다면, 이에 따른 많은 리소스가 발생
      * 연결을 유지하기 위한 리소스를 줄이면 더 많은 연결을 할 수 있으므로 비연결적인 특성 가짐.
   * 단점
      * 서버는 클라이언트를 기억하고 있지 않음
      * 동일 클라이언트의 모든 요청에 대해, 매번 새로운 연결을 시도/해제의 과정을 거침, 연결/해제에 대한 오버헤드가 발생
* #### 무상태 ( Stateless )
   * 비연결성으로 인해 서버는 클라이언트를 식별할 수가 없음.
   * 매번 새로운 인증을 해야하는 번거로움이 발생함.
   * ex) 로그인 -> 연결 -> 응답 -> 연결해제 -> 배너클릭 -> 로그인 -> ~~
   * [로그인을 진행하고 성공하면 로그인 데이터를 유지해야 한다.](#세션과-쿠키)
    

## TCP/IP

* #### TCP

  * 데이터 전달을 관리하는 규칙
  * 데이터를 패킷으로 나누어서 한쪽에서 다른쪽으로 옮기고, 이를 다시 조립하여 원래의 데이터로 만드는 규칙
  * TCP는 패킷을 조립하고, 손실된 패킷을 확인하고, 재전송하도록 요청하는 기능을 함
    
* #### IP
 
  * 인터넷상의 주소 규칙
  * 인터넷상에 연결된 모든 컴퓨터의 위치에도 규칙이 필요함
  * 2⁸X4자리의 주소인 `IPv4`와 16⁴X8자리인 `IPv6`가 있음
    
* #### TCP/IP 4계층
 
  * OSI(Open Systems Interconnections)7계층을 웹 서비스에 맞게 단순화시킨 모델
  * 응용(Application)계층, 전송(Transport)계층, 인터넷(Internet)계층, 물리(Physical)계층으로 나뉨
  * TCP/IP 4계층을 통하여 데이터를 통신하는 순서

    ![img01](https://user-images.githubusercontent.com/55729930/94666195-1f255100-0348-11eb-9584-b8545525b852.jpg)
    * 클라이언트로부터 특정 주소로 요청이 들어오면 DNS 상에서 IP주소를 받아옴.
    * HTTP 계층에서 HTTP 메시지를 작성
    * TCP 계층에서 HTTP 메시지를 패킷으로 분해
    * IP계층에서 전송위치를 확인
    * 네트워크를 통하여 전송
    * 그 이후 위의 과정의 역순으로 진행하여 처리
      
## HTTP header, body

   ![img02](https://user-images.githubusercontent.com/55729930/94673142-42083300-0351-11eb-9924-20adc9d57bf9.jpg)
* #### HTTP header
  * 클라이언트 - 서버 간 일반 문서 데이터(바디 본문) 이외에, 추가적인 정보를 교환할 수 있도록, HTTP 메세지 선두에 삽입되는 요소
  * 요청/응답에 대한 정보는 요청/응답에 대한 일반(General) 정보를 포함한다 (예 : 요청시간, 요청에 사용 된 브라우저 등). 
  * 헤더의 프로퍼티는 `이름 : 값 (Name : Value)` 쌍으로 설정되며, 콜론 `:`으로 구분

* #### HTTP header 유형
  * HTTP 1.1에서 헤더는 세 부분으로 더 나눌 수 있다.
  * 일반 헤더 (General Header)
    * 전송되는 HTTP 본문 컨텐츠와 관련없고, 요청/응답이 생성된 날짜 및 시간 등과 같은 HTTP 통신에 대한 일반적인 정보가 포함.
    * 이 헤더는 HTTP 요청과 응답 메시지에 공통으로 사용. ex) Date:Tue, 17 Nov 2015 16:39:15 GMT
  * 요청 / 응답 헤더 (Request / Response Header)
    * 서버에 요청하면 `요청 헤더`가 있고 서버가 클라이언트/브라우저로 응답을 다시 보낼 때`응답 헤더`가 있다.
    * 요청 헤더는 요청한 URL, 메소드 (GET, POST, HEAD), 요청 생성에 사용 된 브라우저 및 기타 정보와 같은 요청에 대한 정보가 포함된다. ex) User-Agent:"Mozilla / 5.0 (Windows NT 10.0; WOW64; rv : 41.0) Gecko /20100101 Firefox / 41.0 "
    * 응답 헤더 는 사용자가 특정 페이지 또는 리소스에 대한 요청을 보낸 후 서버에서 브라우저에 의해 수신되며 컨텐츠에 사용 된 인코딩, 서버 시스템에서 응답을 생성하는 데 사용되는 서버 소프트웨어 및 기타 정보를 포함한다. ex) Server:nginx
   * 엔터티 헤더 (Entity Header)
    * 이 헤더에는 실제 메시지 또는 전송중인 HTTP 본문에 대한 정보 (컨텐츠 길이, 컨텐츠 언어, 인코딩, 만료 날짜 및 기타 중요한 정보와 같은 정보)가 포함된다. ex) Contents-Length:4959
    
* HTTP body (본문)
  * 가져올 실제 데이터 컨텐츠/메시지 본문이 나타난다. 콘텐츠에는 요청한 리소스에 따라 HTML 코드, 이미지, CSS 스타일 시트 또는 JavaScript 파일이 포함될 수 있다.
      
## Method
* #### HTTP 요청 메소드
  * 클라이언트가 웹 서버에게 특정 동작 수행을 위해 사용자 요청의 목적/종류를 알리는 수단
* #### 요청 종류
  * GET : 존재하는 자원에 대한 요청
    * 파라미터를 넘겨서 해당하는 본문형식을 받는다.
  * POST : 새로운 자원을 생성
    * 클라이언트에서 서버로 전달하고자하는 정보를 서버로 보냄
  * PUT : 존재하는 자원에 대한 변경
    * POST처럼 정보를 서버로 제출하는 것이나 보통 갱신 위주.
  * DELETE : 존재하는 자원에 대한 삭제
    * 웹 리소스를 제거할 때 사용. 
    * DELETE의 경우 서버에서 클라이언트의 요청을 무시 가능, 실제로 삭제되지 않았지만 클라이언트는 파일이 삭제 되었다고 생각할 수 있다.
  * HEAD : 서버 헤더 정보를 획득
    * GET과 비슷하나 Response Body를 반환하지 않음
  * OPTIONS : 서버 옵션들을 확인하기 위한 요청. CORS에서 사용
  
## URL
* #### URL정의
  * 웹 서버가 리소스를 고유하게 식별할 수 있도록 하는 것
  * 특정 서버의 한 리소스에 대해 구체적인 위치를 서술한다.
* #### URL 구조
  * URL은 스킴에 따라 문법이 모두 다르지만, 아래의 구조를 기반으로 선택적으로 사용한다.
  ![img03](https://user-images.githubusercontent.com/55729930/94672517-53047480-0350-11eb-9798-b4e3c945ac2f.jpg)
  * 스킴 ( scheme )
    * 사용할 프로토콜을 말하며, 리소스에 어떻게 요청, 접근할 것인지를 명시한다.
    * 웹에서 주로 HTTP 프로토콜을 사용한다. (ftp, mailto(이메일), rtsp(스트리밍)과 같은 프로토콜을 사용할 수도 있다.)
  * 사용자 이름과 비밀번호
    * 몇몇 서버는 데이터에 접근하기 위해서 사용자의 이름과 비밀번호를 요구한다.
      * ex) ftp://ksh:12345@호스트/asd.xls
    * 만약 사용자이름, 비밀번호를 요구하는 URL 스킴을 사용하는 웹 서버에 클라이언트가 이를 명시하지 않고 URL에 접근 시 기본값으로 "사용자 이름 : anonumous , 비밀번호 : 브라우저 제공 기본 값"을 따르게 됨.
  * 호스트(host)와 포트(port)
    * 하나의 Host에는 여러 개의 Process가 각각의 Socket을 사용하여 데이터 통신시도, 각각의 소켓을 구분할 필요가 있음.
    * 소켓을 구분하는 역할을 하는 것이 포트(Port)
    * HTTP 프로토콜에서 포트 번호를 명시하지 않으면, 80번 포트를 기본 값으로 사용
    * ex) `http://www.google.com:80`
  * 경로
    * 호스트에서 제공하는 자원의 경로를 의미.
    * ex) `https://movie.naver.com/movie/running/current.nhn`
  * 질의
    * Query String( 쿼리 스트링 )이라고도 함.
    * 클라이언트가 자원을 GET 방식으로 요청할 때, 필요한 데이터를 함께 넘겨 줄 목적으로 사용.
      * 개발할 때 함수를 호출하면 파라미터를 던져주는데, 이와 비슷하다고 보면 됨.
      * ex) `http://localhost:3000/index?id=3&page=1`
  * 프래그먼트
    * HTML에는 각각의 요소에 id 속성을 부여가능, URL에 프래그먼트를 전달하면 페이지의 해당 id로 스크롤이 이동.
    * ex) `http://www.naver.com#bottom`
## HTTP 상태 코드
  * #### 정의
    * 서버에서 설정해주는 응답(Response) 정보
  * #### 주요 상태 코드
  
    * 2xx - 성공
    
      * 200 : GET 요청에 대한 성공
      * 204 : No Content. 성공했으나 응답 본문에 데이터가 없음
      * 205 : Reset Content. 성공했으나 클라이언트의 화면을 새로 고침하도록 권고
      * 206 : Partial Conent. 성공했으나 일부 범위의 데이터만 반환
    * 3xx - 리다이렉션
   
      * 클라이언트가 이전 주소로 데이터를 요청하여 서버에서 새 URL로 리다이렉트를 유도하는 경우
      * 301 : Moved Permanently, 요청한 자원이 새 URL에 존재
      * 303 : See Other, 요청한 자원이 임시 주소에 존재
      * 304 : Not Modified, 요청한 자원이 변경되지 않았으므로 클라이언트에서 캐싱된 자원을 사용하도록 권고. ETag와 같은 정보를 활용하여 변경 여부를 확인
    * 4xx - 클라이언트 에러
      * 400 : Bad Request, 잘못된 요청
      * 401 : Unauthorized, 권한 없이 요청. Authorization 헤더가 잘못된 경우
      * 403 : Forbidden, 서버에서 해당 자원에 대해 접근 금지
      * 405 : Method Not Allowed, 허용되지 않은 요청 메서드
      * 409 : Conflict, 최신 자원이 아닌데 업데이트하는 경우. ex) 파일 업로드 시 버전 충돌
    * 5xx - 서버 에러
      * 501 : Not Implemented, 요청한 동작에 대해 서버가 수행할 수 없는 경우
      * 503 : Service Unavailable, 서버가 과부하 또는 유지 보수로 내려간 경우
### URL, 요청 메서드, 상태 코드를 조합
![img04](https://user-images.githubusercontent.com/55729930/94677491-f1e09f00-0357-11eb-9ba1-cd6c264e4680.jpg)

# 2.WebFramework
* #### 웹 프레임워크
   * 동적인 웹페이지나 웹서비스 개발하는 과정에서 DB연동, 템플릿, 세션 관리,  코드 재사용등의 어려움을 줄이는 것이 목적인 프레임워크
   * [MVC 아키텍처 패턴](#MVC-패턴)을 따라 사용자 인터페이스로부터 비즈니스 규칙과 데이터 모델을 분리해 낸다.

* #### 웹 프레임워크 동작 방식

![img06](https://user-images.githubusercontent.com/55729930/94706546-49453600-037d-11eb-9aa6-52f4dd87c9aa.jpg)

   * 라우터: http 메서드와 URL 패턴별로 핸들러를 등록하고, 웹 요청이 들어왔을 때 적절한 핸들러로 연결
      ```
      r.GET("/ping", ping)
      ```

   * 컨텍스트: 웹 요청의 처리 상태를 저장하는 공간이다.

   * 미들웨어: 핸들러 로직을 수행하기 전에 공통으로 수행할 코드 조각이고 재사용이 가능하다. 미들웨어는 주로 다음과 같은 기능을 처리한다.
      * 로그 처리
      * 에러 처리
      * 정적 파일 처리
      * 사용자 인증과 권한 관리
      * 보안 처리
      * 세션 상태 관리
      * 웹 요청 정보 파싱

   * 핸들러: URL별로 정해진 요청을 처리
   ```
   func ping(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "pong",
		})
   }
   ```
 
   * 렌더러: 핸들러 로직 수행 결과를 다양한 형태(JSON, XML, Html Template 등)로 응답
* #### 세션과 쿠키
	* 쿠키
		* HTTP는 무상태(Stateless)을 해결하기 위해 브라우저 단에서 쿠키라는 것을 저장하여 서버가 클라이언트를 식별할 수 있도록 함.
		* 쿠키는 사용자 정보가 브라우저에 저장되기 때문에 공격자로부터 위변조의 가능성이 높아 보안에 취약
	* 세션
		* 세션은 브라우저가 아닌 서버단에서 사용자 정보를 저장하는 구조
		* 쿠키보다는 안전 하지만 세션 정보도 중간에 탈취 당할 수 있기 때문에 보안에 완벽하다고 할 수 없다.
		* 세션을 사용하면 서버에 사용자 정보를 저장하므로, 서버의 메모리를 차지하게 되고, 만약 동시 접속자 수가 많은 서비스일 경우에는 서버 과부화의 원인이 된다.
   
* #### MVC 패턴
	* `M`odel, `V`iew, `C`ontroller의 약자
	
		![img05](https://user-images.githubusercontent.com/55729930/94705341-e3a47a00-037b-11eb-9a61-10c035cdcfa5.jpg)
		* 프로젝트를 효율적으로 진행할 수 있도록 하는 일종의 디자인 패턴, 방법론
		* 웹 어플리케이션을 데이터 처리, UI, 핸들러 등으로 나누고 각 컴포넌트에 집중할 수 있도록 하는 패턴
	* Model
		* 어플리케이션의 정보, 데이터를 담당하는 컴포넌트
		* ex) Database, Business Logic
	* View
		* 사용자 인터페이스를 담당하는 컴포넌트
		* ex) Frontend
	* Controller
		* Model과 View를 잇는 다리역할
		* 사용자 요청에 따라 Model를 적절히 조작, 검색 후 결과를 View를 통해 사용자에게 전달

* #### gin
	* gin.context
		* gin 프레임워크에서 하나의 요청을 처리하는 모든 핸들러에서 함수 인자로 사용하는 변수타입
			* ex) `func TmpHandler(c *gin.Context){ ~ ~ }`
		* http 요청을 처리하는 일련의 과정에서 key:value 형태로 값을 저장 및 조회
			* ex) `c.Request.Header.Get("Accept")`
		* Goroutine의 생성, 중단 등 flow control의 역할 수행
	* gin.context.Param
		* URL Path에 ":"를 지정하면 Gin의 라우터가 파라미터로 처리
		* URL에 지정된 파라미터를 처리함
			*ex) `~~ GET("/view/:article_id", handler.GetArticle)`,`~~ c.Param("article_id") ~~`
	* gin.context.PostForm
		* Post request의 body 값의 form 데이터 조회
			*ex) `title := c.PostForm("title")`
	* gin.H
		* map[string]interface{}와 같음
			* ex) `gin.H{"title": article.Title, "payload": article}`, `gin.H["title"]`
	* gin.Default()
		* Gin 프레임워크의 라우터 생성
	* gin.Default().LoadHTMLGlob("path/*")
		* "./path/" 파일 경로에 있는 html파일들을 요청 처리에 사용할 수 있도록 로드
	* gin.Default().Run("path")
		* 루프백 주소(localhost)의 8080포트로 소켓을 열고 서버를 실행
			* ex) `gin.Default().Run(":8080")`
		* PC의 주소로 서버를 실행 
			* ex) `gin.Default().Run("192.168.10.1:8080")`
	

	
* golang & gin install
```
sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt-get update
sudo apt-get install golang-go
go get -u github.com/gin-gonic/gin
```
