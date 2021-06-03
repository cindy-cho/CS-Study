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

TCP 와 UDP 헤더
-----

TCP :: 3 way hadnshake , 4 way hadnshake
-----

HTTP와 HTTPS
-----

HTTP 요청 응답 헤더
-----

HTTP와 HTTPS 동작 과정
-----

CORS
-----

GET 과 POST
-----

COOKIE 와 SESSION
-----

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