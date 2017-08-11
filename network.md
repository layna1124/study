# Network
우리는 어떻게 다른 컴퓨터와 통신하고, 웹서핑을 할 수 있을까?
컴퓨터간 리소스를 공유 가능하게 만드는 통신망

### Charcteristics
컴퓨터사이의 리소스 공유
네트워크로 연결된 다른 컴퓨터에 접근하여 파일을 생성, 수정, 삭제할 수 있음
프린터와 스캐너, 팩스 등의 출력장치에 네트워크를 연결하여 여러 컴퓨터가 동시 접근 가능

### 네트워크 필요장비 
Network Cable
Distributor(Switch Hub)
Router
Network card


> Router

라우터는 서로 다른 네트워크를 중계하 장치 
수신처 주소를 읽어 적절한 통신통로를 지정 
유지보수 용이, 대규모 통신망을 쉽게 구성 


> 크로스케이블 

랜선을 컴퓨터 2대만 연결해서 데이터 전송할때, 받는선과 보내는선이 달라야 사용이 가능하므로 교차되게 끼우기 

> LAN

Local Area Network(근거리 통신망)
학교, 회사 등 가까운 지역의 좁은 범위

> WAN

Wide Area Network(광역 통신망)
국가, 대륙 등 넓은 지역을 커버

> MAN

Metropolitan Area Network(도시권 통신망)
LAN < MAN < WAN


> WLAN

Wireless Local Area Network(무선 근거리 통신망)
IEEE 802.11 표준을 기반

## Ethernet 
유선 LAN에서 가장 많이 활용되는 기술 규격
이떨넷 (th발음)

# Submarine Cable Map
물리적케이블.
배를 타고 가면서 선을 바다 아래로 내려서 미국까지도 연결되있어 
섬과섬사이도 연결되있어 


> Packet 

: 패킷, 데이터를 한번에 전송할 단위로 자른 데이터묶음 


## Network OSI 7 layer
Open Systems Interconnection Reference Model
국제 표준화기구에서 개발한 컴퓨터 네트워크 프로토콜 디자인과 통신을 계층으로 나누어 설명한 것

![Network OSI 7 layer](https://camo.githubusercontent.com/55bdb3a3951bed828b7c7a161f461468750c415a/687474703a2f2f322e62702e626c6f6773706f742e636f6d2f2d582d6c617477536a5968552f557a724d573266325765492f41414141414141414145382f4933386253535a5a546e632f73313630302f6f7369372e676966)


서버를 통하거나 컴퓨터끼리 통신이 7단계로 이뤄짐
1234 내컴의 네트워크 카드에서 이뤄지고
567 패킷을 분할하고 자름 
보내면 도착해서 반대로 재조립됨  


1. Application layer
: 사용자가 볼수있음, 네트워크활동 인터페이스  
2. Presentation layner
: 전송 받거나 전달되는 데이터의 인코딩과 디코딩
  안전한 데이터 사용을 위한 암호화 
3. Session layer
: 두개의 컴퓨터 사이의 세션이나 대화(dialogue)관리
  모든 통신장비 연결을 관리하고 종료 , 순간적연결끊어짐 막음 
4. Transport layer
: 신뢰성 있는 데이터를 전송할 수 있게 함. 패킷분할 
  흐름 제어, 분할, 재조립, 오류 관리를 포함하지만 
  전송 계층은 지점과 지점 간의 오류가 없음을 보장
  연결 지향적인 프로토콜과 비연결 지향적인 프로토콜을 제공
  방화벽과 프록시 서버가 동작

5. Network layer
: 물리적 네트워크 사이의 라우팅 담당, 
  IP관리. 패킷을 분할해 프로토콜을 식별
  자료의 오류탐지 컴플레인(재요청)
6. Datalink layer
: 실제로 데이터가 전송

7. Physical Layer 
: 네트워크 데이터가 전송될대 사용되는 물리적 매개체 
  전압, 허브 ,네트워크 어댑터 등 
  연결설정을 종료. 공유된 통진자원을 제공

---

## HTTP (HyperText Transfer Protocol)
www상에서 정보를 주고받는 프로토콜
TCP, UDP를 활용
HTTP method: GET, POST, PUT, DELETE

crud만 잘알아도 node.js웹서버 프론트엔드 컨트롤가능 
웹은 리퀘스트를 보내면 리스폰스를 받는것뿐 
프론트엔드는 리스폰스를 해석해서 그림하는것 


### 웹서버 만들때 에러코드처리 
200 번대 잘받았다
300 번대 url이 바꼈는데 반환했다
400 번대 페이지를 찾을수없다
500 서버에서 응답을 보내주지 안았을때 


## FTP (File Transfer Protocol)
서버와 클라이언트 사이에 파일을 다이렉트로 서버에 전송
파일질라 엄청 오래된 프로토콜로 보안30년전것 
서버와 클라이언트 사이에 파일전송을 위한 프로토콜
but, 보안에 매우 취약(패킷 가로채기, 무차별 대입..)
현재는 FTPS(FTP-SSL), SFTP(simple FTP), SSH(Secure SHell) 등을 사용
깃 클론할때 HTTP주소 / 이름 .at하는것 SSH 방법이다른 두가지 
"오늘의 적과싸우지 내일의 적과싸우지안아" =완벽한 보안은 없다는 

## SMTP(Simple Mail Transfer Protocol)
Internet에서 메일을 보내기 위한 프로토콜



# TCP/IP Protocol
전송제어 프로토콜 + 송수신 호스트의 패킷교환을위한 프로토콜 

![Network OSI 7 layer+ tcp/IP Protocol](https://camo.githubusercontent.com/6367e6a2a50124fb1b771d9b179c66ee3ab4a5ef/687474703a2f2f6366696c6532352e75662e746973746f72792e636f6d2f696d6167652f31333433304634363444413930344534313537374131)

Transport 은 2가지 방식 
- TCP방식 (오류없어야 하고 안정적인곳. 서류전송 등 거의 모든경우)
- UDP방식 (돈없고? 바쁘고 실시간이 중요한곳 채팅.게임 )
자르는대로 던져줌. 데이터손실되도 큰 지장없는것들. 스타크래프트 
- 순서가 있고없고의 차이  

## TCP (Transmission Control Protocol)
전송제어 프로토콜
안정적으로/순서대로/오류없이 
빠진것은 다시 요청 처리

- STREAM 
스트림. 각각의 패킷에 번호를 매김 
문자형식의 데이터가 열의 형태로 연속성
- DATAGRAM
하나의 패킷이 발신자와 수신자 정보를 모두담고 있는 독립적 패킷 
순서없이 자르고 어디서보냈고 어디서 받는지만 써있음

> socket

: 두개의 컴퓨터에서 연결을 확인하기위한 절차
- STREAM socket : 연결형, 순서신경 안써도 안정적 데이터 전송
- DATAGRAM socket : 비연결형, 연결해제 과정없이 빠른 데이터 교환가능 

## IP (Internet Protocol)
인터넷 프로토콜 
송수신 호스트의 패킷교환을 위한 프로토콜

### -인터넷 프로토콜 버전 4
현재우리가 사용하는것 32bit비트체제
0또는 1이 8개가 하나의 숫자.
2의8승 256. 컴퓨터는 0부터 시작 이니까 255

문제) 0이 8개면 0 , 1이 8개면 255 이다 
1101 0010 은 몇일까? 
8자리.2진수. 2의7승 2의6승 2의5승 2의4승 2의3승 2의2승 2의1승 2의0승
0빼고 나머지 더하면 210

조합이 43억개 
(70억인구 넘은지2년..한사람들 기기2개이상 ip부족현상으로 ipv6나옴)

### - 인터넷 프로토콜 버전6
Internet protocol version6
이제 공유기 살때 v6지원되는거 사야 20년쓰지 
iot가 활성화 되면서 선풍기에도 ip필요할수있어


127.0.0.0.1  
로컬백 컴퓨터가 가지고 잇는 무조건 반대신호를 반환하는 대역
로컬호스트

학원은 하나의 ip(인터넷아이피) 한주소를 사용해 여러개로 재할당 

192.168.0.x 
로컬아이피 사설네트워크 
내컴퓨터의 ip address


## DNS 
DOMAIN NAME SERVER(SYSTEM)
숫자 4개 외우기 힘들어 판별하기 쉽게 URL을 매핑하는 시스템

인터넷이 안될때. cmd에 핑찍기 신호보기 
$ ping www.google.com 
이때 나오는 172.217.25.68을 주소창에 써도 이동 

기가헤르츠. 피씨방은 200-300대 감당할 껄쓰지만 외부로 나가는IP는 몇개안되 
네트워크카드마다 갖고있는 고유주소가 있기때문에 
13번자리 로그인 .전화번호 주소 남기는걸로 확인. 나쁜짓하면 걸림 


컴퓨터와 연결된 네트워크 정보 확인  
$ ifconfig //맥
$ ipconfig //윈도우
192.168.시작 내로컬아이피주소 나옴 

## Subnetmask
커다란 네트워크를 효율적으로 분배하여 사용할수있도록 도움 
할당받은 하나의 IP주소를 네트워크 환경에 맞춰 적절히 나누어줌
네트워크를 서브넷으로 나누지 않아도 기본적으로 할당
Class C까지 많이씀 255.255.255.0
1111 1111.1111 1111.1111 1111.0000 0000


## UDP (User(Universal) Datagram Protocol)
TCP의 카운터 개념
데이터그램을 전송하기 위한 프로토콜
메시지 수신확인x, 도착순서 예측x  (게임,채팅에 사용)
빠른 속도, 적은 오버헤드

> 오버헤드 

: 와이파이대여폭 사용자기기가 연결될 개수가 한대 추가되면 반이상 속도가 떨어짐 
CPU가 한대일땐 바로쏘는데..데이터가 도착햇을때 어느피시인지 연산하는 순간 속도가 떨어져. 많이쓰는 N604A기기기주 5대가 한계. 안테나많이달린 IP타입공유기를 사야함


## intranet vs Internet vs internet
intranet: internet의 www기술을 활용하여 특정 단체의 내부 정보시스템을 구축하는 것 혹은 그 네트워크 (인트라넷은 내부망, 군대사용)
Internet(International Network): TCP/IP를 활용하여 정보를 주고 받는 통신 네트워크(www)
internet(internetwork): 패킷을 교환하는 방식으로 기기간의 정보를 주고 받는 방식

"internet,email.website 로 ap가 guide발표 : 투쟁하여 Internet 지켜내자~~"


## data
Latin 'Datum"에서 유래

#DB
data의 모임 (어떤 틀이나 표에 갇혀서 삭제,수정,추가가 쉬운 장점)

#DBMS 
.db (파일확장자) 관리 시스템
Oracle
Mysql (오픈소스였음. 썬에게 인수당함. 그뒤로 오라클로 인수당함. 망가트리려했단설)
MariaDB(mysql에서 나온사람들이 만듬. mysql과 명령어같음)


## SQL
structured Query Language
데이터 관리를 위해 설계된 특수목적의 프로그래밍 언어  

![](https://camo.githubusercontent.com/99df2d24061e2c108c73dd3e7e0503bbf18efb07/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f7468756d622f612f61612f53514c5f414e41544f4d595f77696b692e7376672f35353070782d53514c5f414e41544f4d595f77696b692e7376672e706e67)

과거엔 sql이 없어서 자체언어를 썼는데, 맞추기로 프로토콜(약속)하면서 DBMS가 나옴.

데이터베이스와 파일시스템의 차이 
:디비에서 어떤 SQL만 있으면 뭐든지 할수있다.


스키마(구조)

## RDBMS vs NoSQL
- RDBMS
정형데이터. 스키막정.안정적 Mysql, MariaDB NoSQL

- NoSQL
스키마가 없어. 그때바로 추가가능.나중문제점도 없어도 정해놓고 만들어야 안헷갈림 
MongoDB, CouchDB


-------------------------------------------------------


# wireshark 
캡쳐 옵션, 필터, 등을 통해  각 프로토콜, 네트워크 기술별로 패킷을 볼 수 있다
남의 ip주소알라내서 패킷보면 안되용~ 
ip.addr == 192.168.0.1 
80 http 
443 https


# web developer
크롬확장프로그램
css js끄고 웹페이지 테스트 할때 필요 
비밀번호보이기 이런거 



=====================

# 웹의 역사 
1991~2999:
영국 "Tim" Berners-Lee팀버너 world wide web 인터넷환경전체 만듬.(링크) 하이퍼텍스트 기반의 프로젝트를 제안, 
정적인 컨텐츠들을 중심으로 한 웹 기술이 발달

1999~2009: 
동적인서버 
Linux리눅스:운영체제
Apache아파치:서버
Mysql:데이터베이스
php:백엔드언어 
중심의 동적인 서버, 정적인 클라이언트 모델이 지속됨

2010 ~ 현재:
자바스크립트 전성시대 
js엄청 느렸는데 크롬이 나온후 판이 뒤집힘 

넷스케이프(1994)
인터넷익스플로어(1995)가 끼워팔며 점유율 높임
(엑셀, 포토샵 등 오피스를 불법으로 쓰는걸 방조하여 사용률높임)
망했던 네스케이프 자들이 모질라재단 파이퍼폭스(2004)내놓았는데 아직 안망함
검색엔진기반 구글(램괴물..)이 크롬(2008)내놓음
오페라.사파리는 회사꺼. 비발디도 나옴 

# 웹의 구조 

##Client-side

HTML/CSS, javaScript
jQuery, AJAX
Front-end Web Framework
- AngularJS
- React.js
- Vue.js
CSS Framework
- Bootstrap
- Foundation

##Server-side
(Depends on Language)
- PHP: Laravel
- javaScript: Node.js(Express.js)
- Java: Spring
- C++, C#: ASP.net
- Python: Django, Flask
- Golang: itself
- Ruby: Ruby on Rails

##Database
RDBMS
- MySQL
- PostgreSQL
- MariaDB
noSQL
- MongoDB
- CouchDB
- Redis

##etc
- celery (for Distributed Task Queue)
- github, Bitbucket, gitlab (for SCM)
- travis CI or jenkins (for Continuous Integration)
- slack, trello


---
> 트래비스ci  

: 프로젝트때 사용해보기 (튜토리얼많음)
나만쓰는 슬랙방 하나 만들어서 trello, travis 연결
메시지 많이 날라와. 만단위가면 이전자료 지워짐.

> marp 

: 텍스트로 pdf파일 만들기 


- 자바스크립트 클라이언트 부터 백엔드까지 모드 사용가능 언어
- 윈도우도 리눅스시스템 사용가능, 리눅스배쉬 
- backbon.js 앵귤러,리액트,뷰 안나오고 다 만들수 


## URI
인터넷상의 자원을 식별하기 위한 표기법. 상위개념 https://www.example.com/post/how-to-make-url
 - URL: 물리적인위치(프로토콜,아이피.도메인.포트)와 상관있는경우 https://www.example.com/post/ 프로토콜+도메인+자원의 경로명
 - URN: 물리적위치 상관없는경우, www.example.com/post/how-to-make-url




