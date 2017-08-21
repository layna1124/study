# REST API, Socket(TCP, websocket)


# API
Application Program Interface
응용프로그램에서 사용할 수 있도록 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스

ui제공, 윈도우를 사용할때 마우스 키보드등을 통한 사용자의 액션을 하드웨어가 캐치해서 윈도우즈에 신호를 전달. 윈도우즈가 클릭액션 등을 처리

API를 통해 소스 공개는 하지 않으면서 특정권한으로 파일을 업로드/다운로드할 수 있는
기능(인터페이스)을 제공해주는 것 입니다. 바로 이것이 API가 하는 일입니다.
 

## Web API
웹서버 혹은 웹브라우저 위한 API
웹 API는 웹 애플리케이션 개발에서 다른 서비스에 요청을 보내고 응답을 받기 위해 정의된 명세를 일컫는다

## 웹API의 데이터를 가지고 무엇을 할 수 있을까?  
1. 네이버 지도 API를 이용해 내 쇼핑몰에 약도를 넣는다.  
2. 기상청 날씨 API를 이용해 내 쇼핑몰에 날씨를 넣고 싶다.  
3. 네이버 가격비교 API를 이용해 내 쇼핑몰에 가격비교 정보를 넣고 싶다.  
4. 페북이나 트위터 같은 소셜사이트에 콘텐츠를 공유하고 싶다.  
5. 구글 웹로그분석 API를 이용해 쇼핑몰 관리자에 대시보드를 넣고 싶다.  
6. 쇼핑몰에 동영상 등록시 자동으로 유투브에도 발행하고 싶다.  
7. 마이피플을 사용하는 고객과 1:1 상담을 진행하고 싶다.  
8. 카카오톡으로 공유하기 버튼을 넣고 싶다.  

인터넷과 www(world wide web)은 다르다.

## 웹개발 패턴의 변화

1991 ~ 1999:   
하이퍼텍스트 기반의 프로젝트를 제안한 이후 정적인 컨텐츠들을 중심으로 한 웹 기술이 발달
한페이지에 하나의 html필요 

1999 ~ 2009:  
Linux, Apache, Mysql, Php 중심의 동적인 서버, 정적인 클라이언트 모델이 지속됨
동적인 서버환경이 구성되면서 스태틱했던 내용이 변수처리 서버에서정보전달 

2010 ~ 현재:  
javaScript!! (Dynamic Web Client)
스크립트 
예전엔 php개발자가 앞에까지 다했는데 웹환경 복잡해지면서 
클라이어트 개발자 서버개발자 나뉘어있어서 나중에 합침, 소통필요


## SOAP
심플하게 객체에 접근하는 프로토콜 
Simple Object Access Protocol XML 파일 포맷을 활용해 데이터를 주고 받기 위한 시도

## XML
XML에 해더와 바디가 있음
~~~
<?xml version="1.0" encoding="UTF-8"?>
<breakfast_menu>
<food>
    <name>Belgian Waffles</name>
    <price>$5.95</price>
    <description>
   Two of our famous Belgian Waffles with plenty of real maple syrup
   </description>
    <calories>650</calories>
</food>
<food>
</food>
</breakfast_menu>
~~~

## REST API
REpresentational State Transfer Application Programming Interface
Resource : URI 
Verb : HTTP method 
Representations : 표현
표현할수 있는 상태를 전달  


XML구조가 되있어, 리스트업된 문서를 탐색 

레스트는 URI가 맞는값168..
주소를 통해서 리소스에 직적접으로 접근, 서버에 요청하는것
HTTP의 URI를 사용하고 HTTP의 METHOD를 사용한다.  


레스트API를 가져오기 좋은 사이트 망한검색사이트 야후 
주식정보는 야후파이넌스가 갑
애플사의 URI주소를 가져옴 AAPL?p=AAPL
구글GOOG (영문네자리로 회사코드작성)

웹을하면 대용량 아키텍처 하지안는이상 오라클싫어해 
MYSQL(오픈소스1위)인수한 이유가 지위높이려고 


## JSON
자바스크립트의 객체를 표현할때 사용하는 객체형식
데이터를 전달할껀데 {}로감싸고 키,벨류로 되있는것이 특징

## rest 특징
- 웹뿐만 아니라 다른환경에 전달가능 (안드로이드, ios)
 모두 대응위해 rest환경에서 코딩
- 리소스 중심의 api명세 (uri를 읽는것으로 이해가능)
- 클라이언트 상태 신경안쓰고 백엔드에서 데이터를 전달 
잘못하면 데이터꼬임, 클라이언트에서 rest로 통신할때 신경써야함 
- 완벽해 보이지만 표준이 없다. 는 담점이 있다. 
- GET POST PUT DELETE 네개의 메소드로 모든것을 처리 


api설계는 공들여해야. 뭘하는사이트?팔꺼야?
가지들을 만들어놓고 익스프레스로 짜 서버를 빠르게 만듬

크러드라고 부름. http 메소드 4개:

200, 201
400, 404  
500 서버자체가 꺼짐 (코드가 아예전달안된상태이므로 404만처리하면됨)
---
|HTTP||REST|Status Code|
|:--:|:--:|:--:|:--:|
|GET||read|200 OK|
|PUT||update|200 OK|
|POST||create|201 CREATED|
|DELETE||delete|200 OK|

![](https://camo.githubusercontent.com/42d11426217492d79069d78c2adf088f6c334d6e/68747470733a2f2f646162316e6d736c76766e74702e636c6f756466726f6e742e6e65742f77702d636f6e74656e742f75706c6f6164732f323031372f30352f313439343235373437393030322d5265737466756c5365727665722e706e67)


## REST API 설계시 주의할 점

버전관리 https://api.foo.com/v1/bar
명사형 사용 https://foo.com/showid/ --> https://foo.com/user/
반응형 https://foo.com/m/user/, https://m.foo.com/user/ (x)
언어코드 https://foo.com/kr/, https://kr.foo.com/ (x)
응답상태 코드 (200, 400, 500)

적응형이면 m을 따로처리. 반응형이면 필요한가?
m.naver.com 데스크탑에서도 모바일로 보이는 대표적 사이트  
모바일페이지는 네트워크를 쓰니까 한정된 용량안에 쓰니까 용량작게 만들고 
이미지도 리사이즈를 더 심하게 하니까, pc에서 보고싶을때 좋을수있지 안을까  
모바일 디바이스도 커봐야 1000안넘는데 


## RESTful API

스테이터스 코드 정의된대로 쓰기
사용자들의 움직임을 가만해서 설계
uri안에 갇히면 안되. 이용하더라도 메소드를 다르게 전달한다던지 충분히 처리할수있는데
굳이 빼서 deleteuser 해서 U만들지말기.

swagger는 api문서자동화 해주는데 너무 믿지 말기. 오류내포가능성  
<https://www.vmware.com/support/developer/vas/rest-api-1.1.0.RELEASE/index.html#4>


# 실습 : api문서화 하기  
google, H&M, Yahoo 어떠한 액션으로 움직이고 uri가 바뀌는가
실제 api가 어떻게 전달되는가 추측하기 


## postman
크롬익스텐션 확장프로그램   
api테스트, 로컬호스트 테스트, 값이 날아갔을때어떻게 보여주는지 실험가능  
get https://finance.yahoo.com/quote/%5EGSPC?p=^GSPC  해더보면   
주소치면 리스폰스 컨텐츠 타입 넘어오고, 포트뭔지(https 443번) 스테이터스가 어떤지 다나옴.  


## GraphQL
미래 rest api
Open-sourced by Facebook  
Alternative to REST for building APIs  
create strong contract between Client and Server  

----

# Socket 
웹통신에서 중요한 메커니즘
Virtual End Point 기기간에 상호작용을 할수있게 도와주는 가상의 끝점 
포트를 열어놓고 통신을 한다
떨어져 있는 두 컴퓨터를 연결해주는 과정 

전파를 일방적으로 쏘는 라디오 티비  
양쪽이 통신가능하나 한쪽이 보낼때 한쪽은 받기만 하는 무전기는 하프듀플렉스 = 양방향통신  
동시통신이 가능한것은 쌍방향통신 소켓      


Socket() 열기 생성   
bind() 1:1랭귀지 만들고 포트 열기  
Listen() 한쪽이 들어올때까지 기다림  
Accept() 상대쏘켓이 들어오면 받아들임  
Recv() request   
Send() 주고받기   
Close() : 끝나면 다시 listen()으로 쏘켓닫힐때까지 반복  


inet(아이넷은 우리가쓰는인터넷환경)
tcp는 strem,  udp는 datagram 
서버와 클라이언트 맞춰야 통신가능 
웹통신표준 utf8 사용 


## socket 통신보안
TLS : 프로토콜에 의한 암호화   
SSI : 포트에 의한 암호화 


# Websocket 
웹사이트가 사용자와 상호작용하기 위해 만들어진 기술(규격)  
W3C재단이 API를 관리   
port:80, HTTP1.1 
80포트 보안에 취약한가  

## Before 
HTTP Request, Response  
Hidden Frame  
Long Polling (실시간처럼 보일뿐)



## Socket.io

browser 와 상관없이 js를 이용해 실시간 통신을   
브라우저와 웹 서버의 종류와 버전을 분석해 가장 적절한 기술로 통신  
WebSocket, FlashSocket, AJAX Long Polling, AJAX Multi part Streaming, IFrame, JSONP Polling을 적재적소에 사용가능하게함 


  
<https://socket.io>