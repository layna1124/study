# 모던 웹 서비스의 구성요소
# Express Middleware
# Cookie
# Session


# Express Middlware
- 함수
- request 객체, resonse 객체, next함수를 인자로 받음
- 다음 미들웨어를 동작시키기 위해 next함수 
- 라우트핸들러랑 똑같은데 next 있는것 
- 등록된 순서대로 실행되므로 순서중요 
~~~
function helloMiddleware(res, req, next) {
  console.log('hello')
  next()
}

app.use(helloMiddleware)
~~~


## app.use
미들웨어를 앱 전체에서 동작하도록 주입
> app.use(helloMiddleware)

특정 경로에서만 동작하도록 주입
> app.use('/some-path', helloMiddleware)

한 번에 여러 개 주입
> app.use(middleware1, middleware2, middleware3, ...)

## 미들웨어 하는일
- 로깅/ HTTP body를 객체로 변환/ 사용자 인증 (어떠 경로는 로긴해야 쓰기등)/ 권한 관리(로그인을 여러명이 한 어플리케이션에서 내가쓴글만 수정)
- 라우트핸들러로 할수있는 모든일을 할수 있지만 코드재사용 위해 express가 미들웨어(함수)젝오
- 기능 <https://expressjs.com/ko/resources/middleware.html>
- 약3000개 추가중 <https://www.npmjs.com/search?q=express+middleware>



## 실습1 : 미들웨어 
<https://glitch.com/edit/#!/middleware?path=views/index.ejs:1:0>

- ipLoggingMiddleware
- urlLoggingMiddleware
- resLocalMiddleware
- lock : 미들웨어를 만들어 주는 함수 (미들웨어아님)
- app.locals : 앱 단위로 공통적으로 쓰이는 정보를 담는 목적  
- res.locals : 각 요청마다 달라지는 정보를 담는 목적
- 404 페이지 : 라우트 핸들러가 등록된 어떤 경로와도 일치하지 않을 때 맨마지막 미들웨어 실행

### next
호출하면 다음 미들웨어로 처리를 넘김. 미들웨어가 next 함수를 호출하지도 않고, 응답도 보내지 않으면 클라이언트는 응답을 받지 못함. 서버멍때림.


### 함수를 리턴하는 함수 
- 클로저를 이용
- 리턴하는 함수의 성격을 바깥쪽
- 커링 currying 
~~~
function makeAdder(x) {
  return function(y){
    return x + y
  }
}
// undefined
add1 = makeAdder(1)

// f(y){  /*자동함수호출*/
//  return x + y 
// }
add1(2)
// 3 
~~~
같은거 애로우펑션으로 ()안이 안쪽함수, 가로생략가능  
~~~
makeAdder2 = x => (y => x+y)

add5 = makeAdder2(5)
// y => x+y
makeAdder2(3)(4)
// 7
~~~
리액트는 위처럼 함수를 섞고 리턴하고, 함수가 클래스를 리턴하는 등 장난치는 일을 많이해 

## 에러처리 미들웨어
<https://expressjs.com/ko/guide/error-handling.html>
- Bugsnag : 
버그스낵, 에러처리 미들웨어를 만들어줌. 직접짜는 경우보다 이러한 외부서비스 이용. 계정정보 입력해서 미들웨어 주입하기만 하면 바로 쓸수있음.

<br>
---

# Cookie

## 쿠키의 필요성
- 개별적인 클라이언트의 여러 요청에 사이에 같은 정보를 유지시켜야 할때   
- 장바구니/로그인/로그아웃/방문 기록  
- 최초로 그 페이지에 접속 혹은 로그인 했을때, 정보가 브라우저의 저장소에 저장. 내가 서버에 같은 도메인으로 요청을 할때마다 자동으로 포함되어서 전송.


## http cookie
- 서버가 응답을 통해 웹 브라우저에 저장하는 이름+값 형태의 정보 ("넌 로그인을 했어!")
- 웹 브라우저는 쿠키를 저장하기 위한 저장소를 가지고 있음
- 저장소는 자료의 유효기간과 접근 권한에 대한 다양한 옵션을 제공
- ex) 10분뒤에 로그인 풀리기, 특정쿠키는 js에서 접근못하도록, https 보안있어야 접속 등


## 쿠키 전송절차
서버는 브라우저에 저장하고 싶은 정보를 응답과 같이 실어보냄 (Set-Cookie 헤더) 쿠키를 설정하라고 요청 
~~~
HTTP/1.1 200 OK
Set-Cookie: cookieName=cookieValue; Secure; Max-Age=60000
~~~

브라우저는 같은 서버에 요청이 일어날 때마다 해당 정보를 요청에 같이 실어서 서버에 보냄 (Cookie 헤더)
~~~
GET / HTTP/1.1
Cookie: cookieName=cookieValue; anotherName=anotherValue
~~~
쿠키이름=값;

## Set-Cookie 옵션
1. Expires, Max-Age :   
쿠키의 지속 시간 설정  
2. Secure :   
HTTPS를 통해서만 쿠키가 전송되도록 설정
3. HttpOnly :   
자바스크립트에서 쿠키를 읽지 못하도록 설정
4. Domain, Path :  
쿠키의 scope 설정 (쿠키가 전송되는 URL을 지정)  

## Express + Cookie  
(1) 쿠키 읽기 
- req.cookies  
요청에 실려온 쿠키가 객체로 변환되어 req.cookies에 저장됨
cookie-parser 미들웨어 필요    

(2) 쿠키 쓰기 
- res.cookie(name, value)
쿠키의 생성 혹은 수정

## 실습2 : 쿠키 
<https://glitch.com/edit/#!/cookie?path=views/index.ejs:1:0>

1. 현재경로/(server.js에 경로들넣고) 확인 
2. f12 네트워크 set선택, 정보확인 preserve log 체크 
3. f12 Application-storage-cookie


## JS + Cookie
자바스크립트로도 쿠키를 읽고 쓰는 방법이 존재하지만, 보안상 문제
자바스크립트에서 쿠키에 접근하지 못하도록 HttpOnly를 항상 설정하는 것이 best practice

## 쿠키의 한계점
- US-ASCII 밖에 저장하지 못함. 보통 percent encoding을 사용
- 4000 바이트 내외(영문 4000자, percent encoding 된 한글 444자 가량)밖에 저장하지 못함
- 브라우저에 저장됨. 즉, 여러 브라우저에 걸쳐 공유되어야 하는 정보, 혹은 웹 브라우저가 아닌 클라이언트(모바일 앱)에 저장되어야 하는 정보를 다루기에는 부적절

--

# Seesion
쎄션, 시작조건과 종료조건이 있는, 
정보 교환이 지속되는 시간, 또는 회기
셀수있고 시작과 끝이 있는 시간 또는 회기 (몇개다-라고 얘기하니까 )

## 종류 

1. HTTP session  
요청 - 응답   
요청이가서 응답이 올때까지의 시간 
<https://developer.mozilla.org/ko/docs/Web/HTTP/Session> 
> HTTP 같은 클라이언트-서버 프로토콜에서 세션과정 :    
(1) 클라이언트가 TCP 연결을 수립 (2)클라이언트는 요청을 전송한 뒤 응답 기다림 (3) 서버는 요청에 대해 처리, 응답을 상태 코드와 요청에 부합하는 데이터와 함께 돌려보냄

2. 로그인 세션      
로그인 - 로그아웃  
3. Google Analytics 세션      
페이지 접속 - 30분간 접속이 없으면 종료로 간주,커스터마이징 가능
구글 에널리틱스는 사용자 도구 
페이지 사용자수를 측정하는데 어떻게 측정할 것인가?
<https://support.google.com/analytics/answer/2731565?hl=ko>


## 웹 서비스를 위한 세션의 구현
1. 세션이 시작되면(로그인세션으로 예를들면), 세션이 시작되었다는 사실을 쿠키에 저장
2. 세션에 대한 정보를 여러 요청에 걸쳐서 지속시키기 위해, 정보를 어딘가에 저장
3. 세션이 만료되면, 세션이 만료되었다는 사실을 쿠키에 반영


## 세션스토어 
- "세션에 정보를 저장하다" = 세션스토어에 저장한다의 줄임말  
- 세션에 대한 정보를 저장하는 어딘가

서비스의 요구사항에 맞춰서 적절한 저장소를 선택

- 정보의 형태가 간단하고 자주 바뀔 일이 없으면 쿠키
- 저장해야 할 정보의 양이 많으면 데이터베이스
- 정보가 굉장히 자주 변경되면 메모리 기반 저장소


## Express + Session
- cookie-session
쿠키에 모든 정보를 저장하는 세션 스토어. 
첫 방문시 무조건 세션 시작
- express-session
쿠키에는 세션 식별자만 저장하고 실제 정보의 저장은 외부 저장소(데이터베이스 등)를 이용하는 세션 스토어. 외부 저장소에 대한 별도의 설정 필요



## 실습3 : cookie-session 
<https://glitch.com/edit/#!/cookie-session?path=server.js:1:0>
- .env에 문자열넣기 secret세션 정보를 서명할 때 사용할 키 넣어야 에러안남

- session.sig  :
cookie-session 미들웨어는 응답을 보낼 때 session 쿠키에 저장된 문자열을 비밀 키로 서명해서 그 결과를 session.sig 쿠키에 저장



## 실습 4 : cookie-session 인증/인가 
<https://glitch.com/edit/#!/cookie-session2?path=server.js:1:0>
- 인증(Authentication)은 클라이언트 확인, 로그인
- 인가(Authorization) : 권한 설정

- cookie-session미들웨어는 첫 방문시 바로 세션을 시작(guest session) 쿠키에 빈 세션 정보(빈 객체)를 저장. 첫 방문자에 대해서도 session 객체를 바로사용.
- 실습설정 : 로그인 되어있다면 세션에 로그인 이름이 들어있다 
(req.session.username) 쿠키에 저장이 되는 객체 



- 브라우저 열면 js까지 소스전부보여, 보안에 구멍이 생길여지  
- 쿠키세션에 민감한 정보 저장하면 안되 (비밀번호 등)
- 위쪽 계정으로 로그인해서 아래쪽 게정으로 바꿔치기 해볼까? 해킹: 로그인후 f12 세션을 복사(value)하여 base64 디코딩 선택하면 정보 보임. 다시 인코딩해서 붙여넣으면! ..쿠키세션이 보안장치 갖고있어서 안됨.다행임    
- 컨피그세션 쓸때 공개가 되어도 괜찮은 식별자 id정도만 넣어야함

## 해시함수
> hash Function, 긴정보를 짧게하는 변환기     
좋은 해쉬함수는 적당히짧고, 해쉬충돌의 가능성이 적어야함. md5 Hash Generator는  ~하나 붙여도 완전달라짐 
서명을 통한 보안, 암호화 


---



검색 해보기   
(1) curring : 클로저같은, react때 많이사용    
(2) css방법론 bem : react에선 자동화 
css는 전역스코프뿐    
 ul > .todo-list     
 li > .todo-list--itme / .todo-list--item__completed   
