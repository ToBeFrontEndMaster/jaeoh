# http, REST api
> 프로토콜의 정확한 동작 원리와 이론을 알아보자.

> http 스펙과 REST api에 대해서 알아보자.

***
## 목차
>1. 앞서서
>2. http spec
>3. REST api

***
### 1. 앞서서
보통 브라우저는 **클라이언트 프로토콜 및 해석기, 제어기** 이렇게 세 부분으로 나뉘어 집니다.

제어기(보통 하드웨어-키보드, 마우스)로부터 입력을 받아서 브라우저를 통하여 데이터를 전송하고, 데이터를 전송할 때 HTTP, FTP, TELNET과 같은 프로토콜을 사용하여 데이터를 전송합니다. (데이터를 받는 애들 - 클라이언트의 요청마다 웹 서버가 해당하는 웹 페이지들을 보내줍니다! 또한 요즘에는 요청이 많은 파일을 메모리에 캐시를 해준다!!)
이렇게 전송된 데이터는 해석기에 따라 HTML 또는 Java, JavaScript 그리고 Python 등등 많이 있습니다.
문서 해석기는 IE, 넷스케이프 네비게이터, 파이어폭스, 크롬 등등 많은 종류가 있습니다.

이런 웹 페이지에 접근하기 위해서는 클라이언트(유저)는 주소를 필요로 합니다. 전 세계에 퍼져있는 웹 페이지들에 접근을 가능하기 위하여, HTTP는 위치 지정자(resource locator)라는 개념을 사용합니다! URL(Uniform Resource Locator)는 인터넷에서 어떤 종류의 정보든 지정할 수 있는 표준입니다.

![img](https://t1.daumcdn.net/cfile/tistory/2722234356F94DC131)

![img](https://t1.daumcdn.net/cfile/tistory/221FCA3E56F94FB637)

보통 스키마는 프로토콜이라고도 부릅니다.
사용자 이름과 비밀번호가 나오는데, 이는 FTP와 같은 프로토콜을 사용할 때 사용합니다.
그리고 파라미터 같은 경우는 물음표(?)로 시작하고 데이터의 경계를 엔퍼센트(&)로 구분합니다.
경로 뒤에 있는 세미콜론은 CGI를 개발한 벤더회사마다 다릅니다.

 - **프로토콜**은 서버와 대화하기 위하여 사용하는 커뮤니케이션(웹 페이지 혹은 문서를 불러오기) 사용되는 클라이언트 서버 응용 프로그램입니다. 웹 페이지를 불러오는데 프로토콜들도 사용될 수 있습니다. (이중에는 Gopher, FTP, HTTP, News, TELNET 등이 있습니다.)

 - **Host**는 URL이라고 인식하면 쉽습니다. Host는 인터넷 상에 둘도 없는 이름입니다. 이 URL은 IP주소에 매핑됩니다. IP주소는 숫자로 구성되어 있고, 현재 전 세계적으로는 IPv4를 많이 이용하고 있습니다.

 - **Port**를 사용하는 것은 옵션입니다. 만일 포트가 포함된다는 이는 호스트와 경로 사이에 위치해야 합니다. 디폴트 값은 80 port입니다.(HTTP프로토콜이 80번 포트에서 작동하기 때문이라 보면 됩니다!)

 - **Path**는 정보가 위치하고 있는 파일의 경로입니다. 보통 해당 서버가 있는 디렉터리에서의 상대경로를 입력합니다.

 - **파라미터, 질의**는 보통 쿼리스트링이라 부릅니다. GET방식이라면 이 데이터는 URL의 뒷 부분에 파라미터로 쭈욱~~~ 붙어서 날아옵니다. ?마크를 필두로 파라미터 이름과 파라미터값을 한 쌍으로해서 여러쌍일 경우 &로 구분되어서 날라오죠.


WWW에서의 웹페이지는 정적(Static), 동적(dynamic) 및 액티브(active)의 세 분류로 크게 나눌 수 있습니다.
![img](https://t1.daumcdn.net/cfile/tistory/2338604956F9580E03)
정적 문서(static document)들은 보통 개발당시 *.html의 포맷을 갖는 애들을 정적문서라 생각하죠.
클라이언트는 해당 웹 페이지의 복사본만을 얻을 수 있습니다. 다른말로 클라이언트가 내용을 변경할 수 없고, 해당 페이지를 관리하는 서버 관리자 혹은 개발자만이 페이지에 변경을 줄 수 있습니다.
보통 정적문서들은 HTML, XML, XSL, XHTML입니다.
![img](https://t1.daumcdn.net/cfile/tistory/2654FC4556F95B373A)
동적 페이지는 브라우저에서 페이지를 요청할 때마다 웹서버에 의해서 생성됩니다. 요청이 들어오면 웹 서버는 동적 문서를 만드는 응용 프로그램이나 스크립트를 수행합니다. 서버는 프로그램의 출력이나 스크립트를 그 문서를 요청한 브라우저에게 응답으로 반환합니다. 각 요청에 대해 새로운 문서가 생성되기 때문에 동적 문서의 내용은 각각의 요청마다 달라질 수 있습니다. 동적 문서의 예는 네이버나, 구글 홈페이지에서 로그인하면 서버로부터 사용자의 이름, 기타 등등 정보를 받는 것입니다. 동적 페이지에서는 CGI를 빼놓고 이야기 할 수 없습니다.

공통 게이트웨이 인터페이스(CGI: Common Gateway Interface)는 동적 문서를 생성하고 처리하는 기술입니다. CGI는 동적 문서가 어떻게 작성되야 하는지 입력 데이터가 어떻게 프로그램에 제공되어야 하는지, 출력 결과가 어떻게 사용되어야 하는지를 정의하는 표준들 입니다.
CGI는 새로운 언어가 아닌 규약 같은것 입니다. CGI는 언어의 선택은 자유롭게 하되, 따르어야 할 규칙과 용어들의 집합이죠.(개발자가 사용하는 언어에 대해서 제한을 받지 않는다는 뜻입니다!)

보통 데이터는 HTML의 태그인 **\<form>** 태그 Body속에 넣어서 보내주죠. 이것을 폼 파라메터라고도 많이 부릅니다. 

>1. 이렇게 form 태그 속에 있는 데이터들의 양이 적고(URL에는 붙을 수 있는 문자의 최대 길이가 정의되어 있습니다.) 보안과 관련이 없으며, 빠른 속도를 요구하는 Get방식이 있습니다. 서버가 URL을 수신하면, URL부분의 물음표 앞부분으로 사용할 프로그램(페이지)를 선택하고, 물음표의 뒤 부분을 클라이언트의 의해 작성된 데이터로 해석합니다. 이 문자열을 변수에 저장하고, CGI프로그램이 실행될 때 이 변수의 값들을 이용합니다.

>2. 데이터의 양이 많고(payload 에 데이터를 넣죠~ 편지봉투에 데이터를 넣는다 라고도 표현합니다.) Post방식으로 보내주는 경우가 있습니다.

CGI는 서버에서 CGI(Servlet / ASP / PHP etc...)을 실행하고 그 출력을 클라이언트에게 되돌려 주는 것입니다. 보통 되돌려 주는 정보는 HTML의 페이지 혹은 그래픽, 2진데이터, 상태코드 그리고 결과를 캐시하기 위한 브라우저 명령어들 또는 실제 출력 대신 기존의 문서를 전송하기 위한 서버에 대한 명령어들일수도 있습니다.
CGI의 응답은 항상 헤더와 몸체 두부분으로 이루어 집니다. 어떤 CGI 프로그램이든 먼저 헤더, 그리고 빈 줄, 그 이후 몸체가 나옵니다. 그리고 브라우저는 이 헤더를 이용하여 몸체에 어떤 정보가 올 지 해석합니다.


***
### 2. http spec
http란?
> HTTP(HyperText Transfer Protocol), 
[WWW](https://en.wikipedia.org/wiki/World_Wide_Web) 상에서 정보를 주고 받을 수 있는 클라이언트와 서버 사이에 이루어지는 Request/Response 프로토콜이다.

>HTTP는 TCP 위에서 돌아간다고 많이 알려져 있지만 HTTP자체는 상태가 존재하지 않는(stateless)프로토콜입니다.
이것은 클라이언트에 대한 정보가 서버에는 저장되지 않는다는 뜻입니다!
>>HTTP를 설계할 당시, 지구에 있는 모든 장비들이 인터넷과 접속을 하고 있으면, 많은 메모리와 CPU의 성능을 요구했기 때문에 클라이언트는 서버에 연결을 맺고, 요청을 보낸 뒤, 응답을 받습니다. 그리고는 연결을 끊죠. 즉 연결이라고 하는 것은 한 번의 요청과 응답을 위해만 존재한다고 생각할 수 있습니다.

>그렇다는건 지속적인 연결이 아니기 때문에 클라이언트가 두 번째부터 맺는 요청은 서버에게 "나!! 있잖아! 전에 ~~이거 했었던 클라이언트야!" 라는 정보를 흘려줘야 합니다.
이런 문제 때문에 등장한 기술이 세션, 쿠키 입니다!
관련자료는 전에 했었죠? ([seb님 repo](https://github.com/ToBeFrontEndMaster/seb/blob/master/Login_Session%EA%B4%80%EB%A6%AC/Login_Session%EA%B4%80%EB%A6%AC.md))

#### Message format
#### 예제 세션
 - 클라이언트 요청
 ```
 GET /restapi/v1.0 HTTP/1.1
 Accept: application/json
 Authorization: Bearer UExBMDFUMDRQV1MwMnzpdvtYYNWMSJ7CL8h0zM6q6a9ntw
 ```
 - 서버 응답
 ```
 HTTP/1.1 200 ok
 Date: Mon, 23 May 2005 22:38:34 GMT
 Content-Type: text/html; charset=UTF-8
 Content-Encoding: UTF-8
 Content-Length: 138
 Last-Modified: Wed, 08 Jan 2003 23:11:55 GMT
 Server: Apache/1.3.3.7 (Unix) (Red-Hat/Linux)
 ETag: "3f80f-1b6-3e1cb03b"
 Accept-Ranges: bytes
 Connection: close
 
 <html>
 <head>
   <title>An Example Page</title>
 </head>
 <body>
   Hello World, this is a very simple HTML document.
 </body>
 </html>
 ```
##### Request message
클라이언트가 서버에게 보내는 요청 메세지
 - 요청 내용
 > GET /images/logo.gif HTTP/1.1
 - 헤더
 > Accept-Language: en
 - 빈줄
 - 기타 메세지
 ```
 Request-Line
 *(( general-header | request-header | entity-header ) CRLF)
 CRLF
 [ message-body ]
 ```
 
**Request Line**
요청의 첫 줄은 Request Line이라고 부르는데 스펙상은 Method SP Request-URI SP HTTP-Version CRLF 와 같이 정의하는데 보통 다은과 같이 생겼다.
> GET /index.html HTTP/1.1
맨 앞의 GET은 요청 Method를 의미하는데, OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, CONNECT, PATCH 9가지가 있다.


| Method | Action |
| :----- | :----- |
| OPTIONS | 요청 URI에서 사용할 수 있는 HTTP Method를 물어본다. [스펙참고](https://tools.ietf.org/html/rfc2616#section-9.2) |
| GET | 요청 URI의 정보를 가져온다. [스펙참고](https://tools.ietf.org/html/rfc2616#section-9.3) |
| HEAD | GET 요청에서 body는 제외하고 헤더만 가져온다. [스펙참고](https://tools.ietf.org/html/rfc2616#section-9.4) |
| POST | 요청 URI의 리소스의 새로운 정보를 보낸다. [스펙참고](https://tools.ietf.org/html/rfc2616#section-9.5) |
| PUT | 요청 URI에 저장될 정보를 보낸다. [스펙참고](https://tools.ietf.org/html/rfc2616#section-9.6) |
| DELETE | 요청 URI의 리소스를 삭제한다. [스펙참고](https://tools.ietf.org/html/rfc2616#section-9.7) |
| TRACE | 보낸 메세지를 다시 돌려보낸다. [스펙참고](https://tools.ietf.org/html/rfc2616#section-9.8) |
| CONNECT | 프록시에 사용하기 위해 예약된 메서드이다. [스펙참고](https://tools.ietf.org/html/rfc2616#section-9.9) |
| PATCH | partial resource modification 용도.(추가내용) [스펙참고](https://tools.ietf.org/html/rfc5789) |

![img](https://t1.daumcdn.net/cfile/tistory/2556184256FA062F0C)

HTTP1.1스펙에서는 GET, HEAD, PUT 메서드들을 **멱등메서드**라고 정의하고 있습니다.(트랜잭션이 없는것! - 혹은 비동기 적인것!)
여기서 멱등이란 말은 여러가지의 의미를 갖습니다. 동일한 요청은 서버에 어떤 잘못된 결과를 책임지라 하지 않고 수행한다는 이야기 입니다.
트랜잭션을 발생시켜야 하는 메서드는 POST메서드를 사용합니다.

메서드 다음에는 요청 URI가 온다.(/index.html 부분)
말 그대로 URI이고 절대경로의 URI가 될수도 있고 *이 될수도 있다.
Request Line의 마지막에는 HTTP 버전을 의미한다.
마지막에는 <CRLF\>가 있어야 한다. 즉, 줄바꿈을 한다는 얘기인데 CR은 carriage return(13)이고 LF는 linefeed(10)이다. ('\\r\\n')
(각 기호에 대한 정의는 [스펙의 Basic Rule](https://tools.ietf.org/html/rfc2616#section-2.2)에 있다.)

**Headers**
Request-Line 다은에는 header가 위치하는데 general-header, request-header, entity-header 3가지 종류가 있고 요청에 따라 필요한 헤더만 사용하게 된다.

General Header에는 Cache-Control, Connection, Date, Pragma, Trailer, Transfer-Enco, Upgrade, Via, Warning가 있고 Request Header에는 Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match, If-Modified-Since, If-None-Match, If-Range, If-Unmodified-Since, Max-Forwards, Proxy-Authorization, Range, Referer, TE, User-Agent등이 있고 Entity Header에는 Allow, Content-Encoding, Content-Language, Content-Length, Content-Location, Content-MD5, Content-Range, Content-Type, Expires, Last-Modified, extension-header가 있다. 헤더는 name : content의 형식이 되는데 content 부분은 각 헤더에 대한 상세 내용을 확인해 보면 되는데 각 값들은 공백이나 탭으로 구분될 수 있고 각 헤더는 CRLF로 구분된다.
<br>

##### Response message
```
Status-Line
*(( general-header | response-header | entity-header ) CRLF)
CRLF
[ message-body ]
```
첫줄이 요청라인대신에 상태라인인것과 요청헤더 대신 응답헤더가 들어간 것만 빼면 요청 메세지와 동일한 형태이다.

**Status Line**
Status Line은 HTTP-Version SP Status-Code SP Reason-Phrase CRLF로 정의되어 있고 보통 다음과 같이 생겼다.
> HTTP/1.1 200 ok
HTTP 버전은 요청부분에서 설명한 것과 동일하고 상태코드(Status-Code)는 흔히 보는 3자리 숫자로 된 상태를 나타내는 코드로 각 번호대 별로 다음과 같은 의미를 가지고 있다.


HTTP 상태코드 | 내용 | 이유
------------- | ---- | ----
1xx | 정보성 (Informational) | 요청을 성공적으로 받았으며 작업을 계속 진행하고 있다는 뜻 입니다.
2xx | 성공 (Successful) | 200번대 응답은 클라이언트가 요청한 작업을 정상적으로 완료했다는 뜻 입니다.
3xx | 리다이렉트 (Redirection) | 클라이언트가 요청한 페이지가 임시로 다른 페이지로 이동이 되거나, 영구적으로 이동했을 경우 300번 응답을 흘려보냅니다.
4xx | 클라리언트 오류 (Client Error) | 400번대는 클라이언트가 데이터를 잘못 요청하거나 오류가 생겼을 시 서버는 400번대 에러를 흘려보냅니다.
5xx | 서버 오류 (Server Error) | 주로 서버에 용량 부족 혹은 지원하지 않는 서비스를 요청할 당시 많이 발생합니다.

각 상태코드에 대한 [설명도](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

**Headers**
헤더 부분의 General Header와 Entity Header는 요청부분에서 설명한 것과 동일하고, Response Header는 Accept-Ranges, Age, ETag, Location, Proxy-Authenticate, Retry-After, Server, Vary, WWW-Authenticate가 있다. 

***
### 3. REST의 개념
![img](https://gmlwjd9405.github.io/images/network/rest.png)
#### REST란
- REST의 정의
    - "Representational State Transfer"의 약자
        - 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다.
        - 즉, 자원(resource)의 표현(representation)에 의한 상태 전달
    - 월드 와이드 웹(www)과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식
        - REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 **웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.**
        - REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나이다.
- REST의 구체적인 개념
    - HTTP URI(Uniform Resource Identifier)를 통해 자원을 명시하고, HTTP Method를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
        - 즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 자원이 있고 HTTP Method를 통해 자원을 처리하도록 설계된 아키텍쳐를 의미한다.
        - 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.
        - CRUD Operation
            - Create : 생성(POST)
            - Read : 조회(GET)
            - Update : 수정(PUT)
            - Delete : 삭제(DELETE)
            - Head : header 정보 조회(HEAD)
- REST의 장단점
    - 장점
        - HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구축할 필요가 없다.
        - HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
        - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
        - Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
        - REST API 메세지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
        - 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화 한다.
        - 서버와 클라이언트의 역할을 명확하게 분리한다.
    - 단점
        - 표준이 존재하지 않는다.
        - 사용할 수 있는 메서드가 4가지 밖에 없다.
            - HTTP Method 형태가 제한적이다.
        - 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 값이 왠지 더 어렵게 느껴진다.
        - 구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 존재한다.
            - PUT, DELETE를 사용하지 못하는 점
            - pushState를 지원하지 않는 점
- REST가 필요한 이유
    - '애플리케이션 분리 및 통합'
    - '다양한 클라이언트의 등장'
    - 최근의 서버 프로그램은 다양한 브라우저와 안드로이드폰, 아이폰과 같은 모바일 디바이스에서도 통신을 할 수 있어야 한다.
    - 이러한 멀티 플랫폼에 대한 지원을 위해 서비스 자원에 대한 아키텍처를 세우고 이용하는 방법을 모색한 결과, REST에 관심을 가지게 되었다.
- REST 구성요소
    1. 자원(Resource): URI
        - 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
        - 자원을 구별하는 ID는 '/groups/:group_id'와 같은 HTTP URI다.
        - Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태에 대한 조작을 Server에 요청한다.
    2. 행위(Verb): HTTP Method
        - HTTP 프로토콜의 Method를 사용하낟.
        - HTTP 프로토콜은 GET, POST, PUT, DELETE와 같은 메서드를 제공한다.
    3. 표현(Representation of Resource)
        - Client가 자원의 상태에 대한 조작을 요청하면 Server는 이에 적절한 응답을 보낸다.
        - REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 표현으로 나타내어 질 수 있다.
        - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.
- REST 특징
    1. Server-Client 구조
        - 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.
            - REST Server: API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
            - Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
        - 서로간 의존성이 줄어든다.
    2. Stateless(무상태)
        - HTTP 프로토콜은 Stateless protocol이므로 REST 역시 무상태성을 갖는다.
        - Client의 context를 Server에 저장하지 않는다.
            - 즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
        - Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
            - 각 API 서버는 Client의 요청만을 단순 처리한다.
            - 즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
            - 물론 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
            - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.
    3. Cacheable(캐시 처리 기능)
        - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
            - 즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
            - HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
            - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
            - 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.
    4. Layered System(계층화)
        - Client는 REST API Server만 호출한다.
            - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
            - 또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.
        - PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.
    5. Code-On-Demand(optional)
        - Server로부터 스크립트를 받아서 Client에서 실행한다.
        - 반드시 충족할 필요는 없다.
    6. Uniform Interface(인터페이스 일관성)
        - URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
        - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
            - 특정 언어나 기술에 종속되지 않는다.

#### REST API의 개념
![img](https://gmlwjd9405.github.io/images/network/restapi.png)
- REST API란
    - API(Application Programming Interface)란
        - 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환 가능하도록 하는 것
    - REST API의 정의
        - REST 기반으로 서비스 API를 구현한 것
        - 최근 OpenAPI, 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍쳐) 등을 제공하는 업체 대부분은 REST API를 제공한다.
- REST API의 특징
    - 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
    - REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
    - 즉, REST API를 제작하면 델파이 클라이언트뿐 아니라 JAVA, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.
- REST API 설계 기본 규칙
참고 리소스 원형
> - 도큐먼트 : 객체 인스턴스나 DB 레코드와 유사한 개념
> - 컬렉션 : 서버에서 관리하는 디렉터리라는 리소스
> - 스토어 : 클라이언트에서 관리하는 리소스 저장소

    1. URI는 정보의 자원을 표현해야 한다.
        ⅰ. resource는 동사보다는 명사를, 대문자보다는 소문자를 사용한다.
        ⅱ. resource의 도큐먼트 이름으로는 단수 명사를 사용해야 한다.
        ⅲ. resource의 컬렉션 이름으로는 복수 명사를 사용해야 한다.
        ⅳ. resource의 스토어 이름으로는 복수 명사를 사용해야 한다.
            - Ex) GET /Member/1 -> GET /members/1

    2. 자원에 대한 행위는 HTTP Method로 표현한다.
        ⅰ. URI에 HTTP Method가 들어가면 안된다.
            - Ex) GET /member/delete/1 -> DELETE /member/1
        ⅱ. URI에 행위에 대한 동사 표현이 들어가면 안된다. (즉, CRUD 기능을 나타내는 것은 URI에 사용하지 않는다.)
            - Ex) GET /member/show/1 -> GET /member/1
            - Ex) GET /member/insert/2 -> POST /member/2
        ⅲ. 경로 부분 중 변하는 부분은 유일한 값으로 대체한다. (즉, :id는 하나의 특정 resource를 나타내는 고유값이다.)
            - Ex) student를 생성하는 route: POST/students
            - Ex) id=12인 student를 삭제하는 route: DELETE/students/12
- REST API 설계 규칙
    1. 슬래시 구분자(/ )는 계층 관계를 나타내는데 사용한다.
        Ex) http://restapi.example.com/houses/apartments
    2. URI 마지막 문자로 슬래시(/ )를 포함하지 않는다.
        - URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다.
        - REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.
        - Ex) http://restapi.example.com/houses/apartments/ (X)
    3. 하이픈(- )은 URI 가독성을 높이는데 사용
        - 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높인다.
    4. 밑줄(_ )은 URI에 사용하지 않는다.
        - 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 하므로 가독성을 위해 밑줄은 사용하지 않는다.
    5. URI 경로에는 소문자가 적합하다.
        - URI 경로에 대문자 사용은 피하도록 한다.
        - RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문
    6. 파일확장자는 URI에 포함하지 않는다.
        - REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다.
        - Accept header를 사용한다.
        - Ex) http://restapi.example.com/members/soccer/345/photo.jpg (X)
        - Ex) GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg (O)
    7. 리소스 간에는 연관 관계가 있는 경우
        - /리소스명/리소스 ID/관계가 있는 다른 리소스명
        - Ex) GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
-REST API 설계 예시
![img](https://gmlwjd9405.github.io/images/network/restapi-example.png)

#### RESTful의 개념
![img](https://gmlwjd9405.github.io/images/network/restful.png)

- RESTful이란
    - RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 위해 사용되는 용어이다.
        - 'REST API'를 제공하는 웹 서비스를 'RESTful'하다고 할 수 있다.
    - RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
        - 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.
- RESTful의 목적
    - 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
    - RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니, 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.
- RESTful 하지 못한 경우
    - CRUD 기능을 모두 POST로만 처리하는 API
    - route에 resource, id외의 정보가 들어가는 경우(/students/updateName)
***
### 외부 링크
 - [IETF의 HTTP/1.0 기술 명세서 (1996년 5월)](https://tools.ietf.org/html/rfc1945)
 - [IETF의 HTTP/1.1 기술 명세서 (1999년 6월)](https://tools.ietf.org/html/rfc2616)