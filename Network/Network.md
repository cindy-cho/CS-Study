Network
=============

OSI 7 계층 : Application, Prsentation, Session / Transport / Network / Data-Link / Physical
-----
* OSI : Open Systems Interconnection Reference Model
    * 컴퓨터 네트워크 프로토콜 디자인과 통신을 계층으로 나누었다
    * 프로토콜을 기능별로 나누었다
    * 각 계층은 하위 계층의 기능만을 이용하고, 상위 계층에게 기능을 제공한다

* Application / Presentation / Session
    * Applictaion : 응용 계층
        * 응용 프로세스와 직접 관계 하여 일반적인 응용 서비스 수행

    * Presentation : 표현 계층 
        * 코드 간의 번역을 담당
        * MIME 인코딩, 암호화 등의 동작

    * Session : 세션 계층
        * 양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법을 제공
        * Duplex(동시 송수신 방식), Half-Duplex(반이중 방식), Full Duplex(전이중 방식) 통신
        * TCP/IP 세션을 생성, 삭제

* Transport : 전송 계층
    * End to End 사용자들 사이 신뢰성 있는 전송을 보장하기 위한 계층
    * 시퀀스 넘버 기반의 오류 제어 방식
    * 특정 연결의 유효성 제어, Stateful, Connection Oriented
    * 예) TCP
    * 전송 단위 : Segment

* Network : 네트워크 계층
    * 여러개의 노드를 거칠 때 마다 경로를 찾아주는 역할
    * 라우팅, 흐름 제어, 세그멘테이션, 오류 제어, 인터네트워킹 등을 수행
    * 네트워크 관리자가 직접 주소를 할당하는 구조
    * 계층적
    * 전송 단위 : Packet(Datagram)

* Data-Link : 데이터 링크 계층
    * Point to Point간 신뢰성 있는 전송을 보장하기 위한 계층
    * CRC 기반의 오류제어와 흐름제어를 요구
    * 주소 값은 물리적으로 할당 : 네트워크 카드가 만들어질 때 맥주소가 할당
    * 예) 이더넷
    * 전송 단위 : Frame

* Physical : 물리 계층
    * 하드웨어 단계의 전송 기술
    * 높은 수준의 논리 데이터 구조를 기반
    * 전송 단위 : Bit


TCP IP
-----

TCP 와 UDP : Transport Layer 프로토콜
-----
* TCP : Transmission Control Protocol
    * 데이터를 메세지의 형태로 보내기 위해 IP와 함께 사용하는 프로토콜
    * 연결형 서비스 : 가상 회선 방식 제공
        * 연결 설정 : 3-way handshaking
        * 연결 해제 : 4-way handshaking
    * 흐름 제어 및 혼잡 제어
        * 흐름 제어
            * Receiver와 Sender의 데이터 처리 속도를 조절하여 Receiver의 버퍼 오버플로우를 방지
            * Sender에서 많은 데이터를 빠르게 보내 Receiver에서 문제가 일어나지 않도록 방지
        * 혼잡 제어
            * 네트워크의 패킷 수가 넘치지 않게 방지
    * 높은 신뢰성을 보장 : 신뢰성 > 연속성
    * UPD 보다 느리다
    * Full-Duplex : 전송이 양방향으로 일어날 수 있다
    * Point to Point
    * 멀티캐스팅 또는 브로트캐스팅을 지원하지 않는다
    
* UDP : User Datagram Protocol
    * 데이터를 데이터그램 단위로 처리
    * 비연결형 서비스
        * 연결을 위해 할당되는 논리적 경로가 없다
        * 각각의 패킷은 독립적인 관계를 가진다
    * 정보를 송수신 할 때 사인을 교환하지 않는다
    * 헤더의 CheckSum 필드를 통해 최소한의 오류만 검출
    * 낮은 신뢰성
    * TCP 보다 속도가 빠르다
    * 실시간 서비스, 스트리밍의 경우에 이용

* 참고
    * TCP 와 UDP는 각각 별도의 포트 주소 공간을 관리하기 때문에 같은 포트 번호를 사용해도 무방
    * 같은 모듈 내에서도 (TCP, UDP) 클라이언트에서 동시에 여러 커넥션을 확립한 경우에는 서로 다른 포트 번호를 동적으로 할당

TCP 와 UDP 헤더 : 상위 계층으로 데이터를 받아 헤더를 추가한다
-----
* TCP 헤더 : (크기 bits)
    * (16) Source Port, Destinatin Port : 포트 주소
    * (32) Sequence Number : Sender가 지정하는 번호, 전송되는 바이트 수 기준으로 증가
    * (32) ACK Number : 제대로 수신한 바이트 수
    * (4) Header Length (Data Offset) : TCP 헤더 길이, 4바이트 단위 표시
    * (6) Resv (Reserved) : 0으로 채워진 예약 필드
    * (6) Flag Bit
        * URG : 긴급 위치 필드 유효 여부
        * ACK : 응답 유효 (데이터를 잘 받았으면 SYN + 1 = ACK 으로 전송)
        * PSH : Receiver측에 버퍼링된 데이터를 상위 계층에 즉시 전달할 때
        * RST : 연결 리셋 응답 혹은 유효하지 않은 세그먼트 응답
        * SYN : 연결 설정 요청. 최초 패킷에만 SYN 플래그 설정
        * FIN : 연결 종료 의사 표시
    * (16) Window Size : 수신 윈도우의 버퍼 크기 (0이면 송신 중지)
    * (16) TCP Checksum : 헤더와 데이터의 에러 확인 용도
    * (16) Urgent Pointer : 현재 순서 부터 표시된 바이트까지 긴급한 데이터임을 표시. URG가 유효할 경우에만 사용
    * (0~40) Options : 추가 옵션 있을 경우 표시

* UDP 헤더 : (크기 bits)
    * (16) Source Port, Destination Port : 포트 주소
    * (16) Length : 헤더 + 데이터 포함 전체 길이
    * (16) CheckSum : 헤더와 데이터 에러 확인 용도

TCP : 3 way hadnshake, 4 way hadnshake
-----
* 3 way handshake : 네트워크 연결을 설정 (Connection Establish)
    * 순서
        * Client -> Server : (Seq=n, SYN)
        * Server -> Client : (Seq=m, ACK(n+1), SYN, ACK)
        * Client -> Server : (Seq=n+1, ACK(m+1), ACK)

* 4 way handshake : 네트워크 연결을 해제 (Connection Termination)
    * 순서
        * Client -> Server : (FIN)
        * Server -> Client : (ACK)
        * Server -> Client : (FIN)
        * Client -> Server : (ACK)

* PORT State
    * CLOSED : 포트가 닫힌 상태 
    * LISTEN : 포트가 열린 상태로 연결 요청 대기 중
    * SYN_RCV : 요청을 받고 상대방의 응답을 기다리는 중
    * ESTABLISHED : 포트 연결 상태

* Related Question
    * TCP 연결 설정 과정에서 3 way 와 4 way 로 차이가 나는 이유는 ?
        * 연결을 종료할 경우에, 클라이언트는 요청이 끝났다 하더라도 서버 쪽에서는 보내야할 데이터가 남아있을 수 있기 때문에, 종료요청(FIN)에 대한 ACK만을 보낸후, 데이터 전송이 완료된 후 FIN을 보내기 때문이다.
    
    * Server에서 FIN을 전송전에 전송한 패킷이 Routing 지연이나 Packet Loss로 인한 재전송으로 인해 FIN 보다 늦게 도착하는 상황이 발생하면 어떻게 되는가 ?
        * 이러한 현상에 대비하여 Client는 Server로 부터 FIN을 수신하더라도 일정시간(Default : 240sec)동안 세션을 남겨 놓고 잉여 패킷을 기다리는 과정을 거친다. (TIME_WAIT)

    * 초기 Sequence Number인 ISN을 0 부터 시작하지 않는 이유는 ?
        * Connection을 맺을 때 사용하는 포트는 유한한 범위 내에서 사용하고 시간이 지남에 따라 재사용 된다. 따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용할 가능성이 존재한다. 서버 측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데 난수가 아닌 순차적인 Number가 전송된다면 이전의 Connection으로부터 오는 패킷으로 인식할 수 있다. 이런 문제가 발생할 가능성을 줄이기 위해 난수를 생성해서 설정한다.

HTTP와 HTTPS : HyperText Transfer Protocol (over Secure Socket Layer)
-----
* HTTP 프로토콜 : HyperText Transfer Protocol
    * 웹 상에서 Client와 Server 간에 request/response로 정보를 주고 받을 수 있는 프로토콜
    * 특징
        * 주로 HTML 문서를 주고 받는데 사용
        * TCP, UDP 사용, 80번 포트 사용
        * Connectionless : Client가 요청을 보내고 Server가 응답을 하면 연결이 끊어진다
        * Stateless : 연결을 끊는 순간 통신은 끝나며 상태 정보를 유지하지 않는다

* HTTPS 프로토콜 : HyperText Transfer Protocol over Secure Socket Layer
    * 웹 통신 프로토콜인 HTTP의 보안이 강화된 버전
    * 특징
        * 기본 TCP/IP 443번 포트 사용
        * 웹 상에서 정보를 암호화 하는 SSL이나 TLS프로토콜을 통해 세션 데이터를 암호화 한다
            * SSL(Secure Socket Layer)
            * TLS(Transport Layer Security) : SSL에서 발전한 프로토콜
            * SSL, TLS는 사생활 보호, 데이터 무결성, ID 및 디지털 인증서를 사용한 인증 제공
        * 데이터의 적절한 보호 보장
            * 보호의 수준은 웹브라우저에서의 구현 정확도와 서버 소프트웨어, 지원되는 암호화 알고리즘에 달려있다
    * 원리
        * 공개키 알고리즘 방식
        * 공개키, 개인키를 이용한 암호화 방법
            * 공개키 : 모두에게 공개, 공개키 저장소에 등록
            * 개인키(비공개키) : 개인에게만 공개. Client-Server에서는 Server가 비공개키를 가지고 있다
        * Client -> Server
            * 사용자의 데이터를 공개키로 암호화
            * 서버로 전송 (데이터를 가로채도 개인키가 없으므로 복호화 불가)
            * 서버의 개인키를 통해 복호화하여 요청 처리
    * 장점
        * 네트워크 상에서 열람, 수정이 불가능하기 때문에 안전하다
    * 단점
        * 암호화 과정에 웹서버에 부하를 준다
        * 설치 및 인증서 유지에 추가 비용 발생
        * HTTP에 비해 느리다
        * 인터넷 연결이 끊긴 경우 재인증 시간이 소요된다

HTTP 요청 응답 헤더
-----
* General Header : 요청 및 응답 메세지 모두에서 사용 가능한 기본 헤더 항목
    * Date : HTTP 메시지 생성 일시
    * Connection : 연결에 대한 옵션 설정
    * Cache-Control
    * Pragma
    * Trailer

* Entity Header : 요청 및 응답 메세지 모두에서 사용 가능한 Entity 설명 헤더
    * Content-Type : 미디어 타입, 문자 인코딩 방식
    * Content-Encoding : 데이터 압축 방식
    * Content_Length : 데이터 길이 (Bytes)
    * Content-Location
    * Content-Disposition : 브라우저 표시 방식, inline - 화면 표시, attachment - 다운로드
    * Content-Security-Policy : 다른 외부 파일을 불러오는 경우 차단할 소스와 불러올 소스 명시
    * Location : 리다이렉트 된 때에 이동된 주소, 새로 생성된 리소스 주소
    * Last-Modified : 리소스를 마지막으로 갱신한 날짜

* Request Header : 요청 메세지
    * Host
    * User-Agent
    * From
    * Cookie
    * Referer
    * If-Modified-Since
    * Authorization
    * Origin
    * Body 속성
        * Accept
        * Accept-Charset
        * Accept-Encoding
        * Accept-Language

* Response Header : 응답 메세지
    * Server
    * Accept-Range
    * Set-Cookie
    * Expires
    * Age
    * ETag
    * Proxy-Authenticate
    * Allow
    * Access-Control-Allow-Origin

HTTP와 HTTPS 동작 과정
-----
* HTTP 동작 과정
    * 서버 접속 -> 클라이언트 -> 요청 -> 서버 -> 응답 -> 클라이언트 -> 연결 종료
    1. 사용자가 웹 브라우저에 URL 주소 입력
    2. DNS 서버에 웹 서버의 호스트 이름을 IP 주소로 변경 요청
    3. 웹 서버와 TCP 연결 시도 : 3-way Handshaking
    4. 클라이언트가 서버에게 요청
        * HTTP Request Message = Request Header + 빈 줄 + Request Body
            * Request Header = Method + URL + Protocol Ver
            * 빈 줄
            * Request Body
    5. 서버가 클라이언트에게 데이터 응답
        * HTTP Response Message = Response Header + 빈 줄 + Response Body
            * Response Header = Protocol Ver + Code + Message
            * 빈 줄
            * Response Body
    6. 서버-클라이언트 연결 종료
    7. 웹 브라우저가 웹문서 출력

* HTTPS 동작 과정
    * 공개키 암호와 방식과 대칭키 암호화 방식의 장점을 활용한 하이브리드 사용
        * 데이터를 대칭기 방식으로 암복호화 하고, 공개키 방식으로 대칭키 전달
    1. 클라이언트가 서버에 접속, Handshaking 과정에서 서로 탐색
        1.1. Client Hello
        1.2. Server Hello
        1.3. Client 인증 확인
        1.4. Server 인증 확인
        1.5. Handshaking 종료
    2. 데이터 전송
    3. 연결 종료 및 session key 폐기

CORS : Cross Origin Resource Sharing
-----
* CORS : 웹 서버에게 보안 cross-domain 데이터 전송을 활성화하는 접근 제어권 부여
* 과정
    1. Options 주소로 서버가 CORS를 허용하는지 물어본다
    2. Access-Control-Request-Method로 실제로 보내고자 하는 method를 알린다
    3. Access-Control-Request-Header로 실제로 보내고자 하는 header를 알린다
    4. Allow 항목은 Request에 대응되는 것으로, 서버가 허용하는 method와 header 응답에 사용
    5. Reqeust와 Allow가 일치하면 CORS 요청이 이루어진다

GET 과 POST : 서버에 데이터를 전달할 때 사용하는 방식
-----
* GET
    * 개념
        * 정보를 조회하기 위한 method
        * 서버에서 어떤 데이터를 가져와서 보여주기 위한 용도
        * Select
    * 사용 방법
        * URL 끝에 '?', 요청 정보는 (Key, Value)로 쌍을 이루어 ? 뒤에 붙어서 서버로 전송
        * 요청 정보가 여러 개일 경우에는 & 로 구분
    * 특징
        * URL에 요청 정보를 붙여서 전송
        * URL에 붙이기 때문에 길이 제한이 있어 대용량 데이터 전송이 어렵다
        * 요청 정보를 사용자가 눈으로 확인 가능 (POST 보다 보안상 취약)
        * HTTP 패킷의 Body는 비어있는 상태로 전송
        * POST 보다 빠르다
        * 캐싱 사용 가능

* POST
    * 개념
        * 서버의 값이나 상태를 바꾸기 위한 method
        * Insert, Update, Delete
    * 사용 방법
        * 요청 정보를 HTTP 패킷의 Body에 숨겨서 서버로 전송
        * Request Header의 Content-Type에 해당 데이터 타입 표현
    * 특징
        * 대용량 데이터 전송에 적합
        * 클라이언트는 인코딩 하여 서버로 전송, 서버는 디코딩 한다
        * GET 보다 보안상 안전

* Related Question
    * 조회하기 위한 용도로 POST 가 아닌 GET 방식을 사용하는 이유?
        * 설계 원칙에 따라 GET 방식은 서버에게 여러번 요청 하더라도 동일한 응답이 돌아와야 한다
            * GET 은 가져오는 것으로 서버의 데이터나 상태를 변경시키지 않아야 한다
            * POST 는 수행하는 것으로 서버의 데이터나 상태를 바꾸기 위한 용도이다
        * 웹에서 모든 리소스는 Link할 수 있는 URL을 가지고 있어야 한다
            * POST 방식을 사용할 경우 URL 정보가 Body에 있기 때문에 URL만 전달 할 수 없다.

COOKIE 와 SESSION :  🍪
-----
* COOKIE
    * 개념
        * 클라이언트 로컬에 저장되는 키와 값이 들어있는 파일
        * 이름, 값, 유효 시간, 경로 등을 포함
    * 구성 요소
        * Name, Value, Expires, Domain, Path, Secure, HttpOnly
    * 동작 과정
        1. 웹브라우저가 서버에 요청
        2. 상태를 유지하고 싶은 값을 Cookie로 생성
        3. 서버가 응답할 때 HTTP 헤더에 Set-Cookie에 Cookie를 포함하여 전송
        4. 전달받은 Cookie는 웹브라우저에서 관리하고 있다가, 다음 요청 때 HTTP 헤더에 Cookie를 넣어서 전송
        5. 서버에서는 Cookie 정보를 읽은 후 응답

* SESSION
    * 개념
        * 일정 시간 동안 동일 브라우저로부터 들어오는 요청을 하나의 상태로 보고 그 상태를 유지 한다
    * 동작 과정
        1. 웹르라우저가 서버에 요청
        2. 서버가 해당 웹브라우저에 Session ID 부여
        3. 서버가 응답 시 HTTP 헤더에 Session ID를 포함하여 전송
        4. 웹 브라우저 닫기 전까지는 부여된 Session ID를 HTTP 헤더에 넣어서 전송
        5. 서버는 Session ID를 확인 후 응답

* 세션도 쿠키를 사용하여 값을 주고받으며 클라이언트의 상태 정보를 유지한다

* 비교
    |           | 쿠키         |세션                |
    |-----------|-------------|-------------------|
    | 저장 위치   | 클라이언트     | 서버               |
    | 보안       | 취약         | 비교적 좋다          |
    | 라이프사이클 | 만료시간에 따른다| 브라우저 종료        |
    | 속도       | 빠르다        | 느리다 (서버 처리 필요)|

DNS
-----

REST와 RESTUful
-----

SOCKET
-----

Socket.io 와  Websocket
-----

Frame Packet Segment Datagram
-----