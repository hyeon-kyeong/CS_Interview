# HTTP & HTTPS

### HTTP(HyperText Transfer Protocol)

* HTTP란?

    HyperText 문서를 교환하기 위한 응용 계층 프로토콜

    웹 서버와 클라이언트 간의 데이터를 주고받기 위해 만들어놓은 통신 규약

* HTTP 특징

1. 초반에는 HTML과 같은 하이퍼미디어 문서를 주로 전송했지만 최근에는 Plain text, JSON, XML 등 다양한 형태의 정보도 전송함

2. 웹 브라우저와 웹 서버 간의 커뮤니케이션을 위해 디자인되었지만, 최근에는 모바일 애플리케이션, IoT와의 커뮤니케이션 등과 같이 다양한 목적으로도 사용됨

3. 클라이언트가 요청을 생성하기 위해 연결을 연 다음 응답을 받을 때까지 대기하는 <b>클라이언트-서버 모델</b>임

4. 무상태(Stateless) 프로토콜임\
    서버가 두 요청 간에 어떠한 상태나 데이터를 유지하지 않음\
    (상태를 유지하기 위해서는 Cookie와 Session을 사용함)

5. 일반적으로 안정적인 TCP/IP를 기반으로 사용함

6. port 번호 : 80

* HTTP 동작 방식

    클라이언트(웹 브라우저, 모바일 등)가 브라우저를 통해 어떠한 서비스를 URI를 통해 서버에 요청(Request)하면 서버에서 해당 요청에 대한 결과를 응답(Response)하는 형태

    * 클라이언트 : 서버에게 요청을 보내는 리소스 사용자\
        ex) 웹 브라우저, 모바일 애플리케이션, IoT 등

    * 서버 : 클라이언트에게 요청에 대한 응답을 제공하는 리소스 관리자

1. TCP Connection

    TCP 연결은 요청을 보내거나 응답을 받는데 사용됨

    클라이언트는 새 연결을 열거나, 기존 연결을 재사용하거나, 서버에 대한 여러 TCP 연결을 열 수 있음

2. HTTP 메세지 전송

3. 서버에 의해 전송된 응답을 읽음

4. TCP Connection을 close 하거나 다른 요청을 위해 재사용함

* HTTP 메세지

    * 요청

            GET/HTTP/1.1
            Host: developer.mozilla.org
            Accept-Language: fr

        GET : Method\
        / : Path\
        HTTP/1.1 : Version of the protocol\
        Host ~ fr : HTTP Request Headers, 리소스를 요청하고자 하는 경로로 요청하고자 하는 서버의 도메인을 적음\
             해당 예시는 HTTP의 기본 port인 80번 port를 사용하기 때문에 port 번호가 생략됨

    * 응답

            HTTP/1.1 200 OK
            Date : Sat, 09, Oct 2010 14:28:02 GMT
            Server: Apache
            Last-Modified: Tue, 01, Dec 2009 20:18:22 GMT
            ETag: "51142bc1-7449-479b075b2891b"
            Accept-Ranges: bytes
            Content-Length: 29769
            Content-Type: text/html

        HTTP/1.1 : Version of the protocol\
        200 : Status code\
        OK : Status message\
        Date ~ text/html : HTTP Response Headers

* HTTP 요청 메소드

        1. GET : 클라이언트가 서버에 리소스를 요청할 때 사용 (CRUD에서 Read)
        2. POST : 클라이언트가 서버의 리소스를 새로 만들 때 사용 (CRUD 에서 Create)
        3. PUT : 클라이언트가 서버의 리소스를 수정 할 때 사용 (CRUD에서 Update: 전체 수정)
        4. DELETE: 클라이언트가 서버의 리소스를 삭제 할 때 사용 (CRUD에서 Delete)

        etc : PATCH, HEAD, OPTIONS, CONNECT, TRACE 등

* HTTP 상태 코드 정보

        1xx(정보) : 요청을 받았으며 프로세스를 계속해서 진행함
        2xx(성공) : 요청을 성공적으로 받고 인식했으며 수용함
        3xx(리다이렉션) : 요청 완료를 위해 추가 작업 조치가 필요
        4xx(클라이언트 오류) : 요청의 문법이 잘못되었거나 요청을 처리할 수 없음
        5xx(서버 오류) : 서버가 명백히 유효한 요청에 대한 충족을 실패

* 보안 문제

    암호화가 되지 않은 텍스트를 전송하는 프로토콜이기 때문에, 네트워크에서 신호를 가로채면 내용이 노출되는 보안 문제가 존재함

    => 해당 문제를 해결하기 위한 프로토콜이 HTTPS임

### HTTPS(HyperText Transfer Protocol Secure)

* HTTPS란?

    HTTP에 데이터 암호화가 추가된 프로토콜

    인터넷 상에서 정보를 암호화하는 SSL 프로토콜을 사용하여 클라이언트와 서버가 자원을 주고 받을 때 사용하는 통신 규약

* HTTPS 특징 

1. HTTP에 Secure Socket이 추가된 형태로, 기존의 HTTP 통신에 SSL 혹은 TLS 프로토콜을 조합해 세션 데이터를 암호화함

2. 공개키 암호화 방식 사용

3. port 번호 : 433

* HTTP 동작 방식

1. 클라이언트는 서버에 접속하며 서버 인증서(CA : Certificate Authority)를 받음

2. 서버 인증서 신뢰 여부 체크 후, 공개키를 추출함

3. 클라이언트는 서버와 통신하는 동안만 사용할 대칭키를 만들고, 해당 대칭키를 서버의 공개키로 암호화한 후 서버로 전송함

4. 서버는 암호화된 대칭키를 자신의 개인키로 복화하해 클라이언트와 동일한 대칭키를 추출하고, 해당 대칭키를 이용해 클라이언트와 통신함
