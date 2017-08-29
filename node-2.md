# HTTP심화, 웹서버개론, Express

## wire shark
컴퓨터에는 수많은 컴퓨터 장치가 있다. 각각의 랜선꼽는곳 블르투스 등
특정 장치하나를 골라서 모든 트래픽을 감시할수 있는 도구
http가 어떻게 생겼는가 볼수있다

## Chrome Devtools
개발자도구-네트워크-필터-Name-header
정보 동일하게 볼수있다


## HTTP 라는 프로토콜
- 웹브라우저와 웹서버간의 통신을 위한 규약 
- 텍스트 형식으로 통신 (0101로 통신이 기계에는 효율적이지만 사람이 디버깅 하기쉬우라고 )
- 최근 REST API의 부상으로 널리사용 
(모바일앱 서버간의 통신)
- 80번 포트를 기본 사용 
- 클라이언트의 요청과 서버의 응답으로 이루어짐 
- 1999년 발표된 HTTP 1.1이 현재까지 많이사용 


## HTTPS
- https:// 보안프로토콜은 와이어샤크에서 정보확인이 안된다.
- HTTP통신을 암호화해 중간에서 주고받는 내용을 가로챌수 없게함
- 443번 포트를 기본사용

## HTTP/2
- 통신속도 개선
- 텍스트 기반아님 
- HTTPS를 써야함
- 현재 16% 점유 

보여주기만 하는 사이트는 HTTP로 문제없으나 개인정보 많은 사이트는 HTTPS를 사용해야 한다.

## 응답과 요청
- 웹브라우저는 웹서버에 요청을 보냄
- 그에따라 서버는 클라이언트에 응답을 보냄
- 웹브라우저는 html문서 형태의 문답이 오면, 분석후 요청을 각각 추가로 보냄(css, js, 폰트, 오디오)

## 요청 Request Methods
- 서버에 자료를 보낼때 쓰는 요청의 종류 8가지
- get/post/head/put/delete/connect/options/patch/..trace
- 읽어보기 <https://developer.mozilla.org/ko/docs/Web/HTTP/Methods>

- 특정 상황에서 특정 메소드로 요청하도록 만들어짐
- 웹브라우저는 순수 html만으로는 get, post밖에 지원하지 않지만, ajax처럼 요청을 보내는 코드를 직접짤때는 메소드 선택가능
- 자료본문을 요청하는 get메소드, 새로은자료 post메소드가 가장 많이 쓰임 

### 서버가 충족시켜야하는 메소드의 성질
- Safe : 읽기전용 , get은 읽기전용만 사용하도록 표준에 명시 
- Idempotent : 네트워크가 불안정해도 안전하게 요청을 보낼수 있다. 네트워크는 신뢰할수없어. 여러번 같은 요청해도 한번한 한것으로 처리되어야함   
( put요청한 자료를 통째로 바꿔달라, 여러번보내고 같은결과가 와야하니까 idempotent성질 만족yes해야함 /  patch는 리소스의 부분만을 수정할때 쓰기때문에 no여도됨)
- Cacheable : 특정조건 만족시 응답을 클라이언트에 저장했다가 다음요청때 다시 사용가능


## url구성요소 
![](https://cascadingmedia.com/assets/images/insites/2015/02/url-anatomy/url-anatomy-55598c24.png)

5. 80포트 아닐대 직접써줘야
2~5는 서버의 위치, /path/ 경로  6부터는 서버에서 얻고싶은 자원의 서버내의 위치 
7. 쿼리스트링, ?이름=값  여러개 보낼수있어
8. 해쉬체인지 #setion-id


## percent encoding 
url은 아스키문자 밖에 사용못함으로 non-ascii 표준인코딩
방법이 나옴 
~~~
> encodeURIComponent("한글")
"%ED%95%9C%EA%B8%80"
> decodeURIComponent("%ED%95%9C%EA%B8%80")
"한글"
~~~
프레임워크 라이브러리를 쓰면 자동으로 됨

## request target
요청타겟 
> GET /path/to/resource?foo=bar&spam=hoge#fragid HTTP/1.1


## Response status
http 응답상태코드 
> HTTP/1.1 200 OK

<https://httpstatuses.com/>
: 개발자 스러운 내용을 예쁘게 만들어서 유명해진 사이트

* 2xx 성공 
  * 200 ok 
  * 201 created 자료가 성공적으로 생성 
* 3xx 추가작업필요
  * 301 자료가 완전히 다른곳 이동해서 나에게 없어 
  * 302 자료 일시적으로 다른곳에 있다 
  * 304 Not modified 캐시위해 사용되는 응답코드, 전에받은것 그대로써(css js img 들)
* 4xx 실패 클라이언트 책임
  * 400 요청이 잘못됫음 (이상한방식, 필요자료없거나)
  * 403 자료 접근권한 없음 
  * 404 자료가 없고 어디있는지 모르겠고 잘못된 요청을 보낸거같아 
* 5xx 실패 서버책임
  * 500 요청은 잘 들어왔지만 서버 로직쪽에서 에러, 개발자가 예상지 못한 에러가 났을때 클라이언트에 보내는  
  * 503 일시적 응답없음, 요청너무 많을때 


# HEADER
요청과 응답에 대한 추가정보를 표현  
인증, 캐싱, 쿠키, 보안, 프로시 등

- Authorization
어써라이제이션, 요청의 인증 정보
- User-Agent
요청중인 클라이언트의 정보 
클라이언트가 크롬인지 익스인지 판별, 구글 네이버 빙 같은
검색엔진이 크롤러들(구글봇 1.2)인지 판별, 크롤링하는거 싫으면 차단도 하고 
- Locatinon
301, 302응답에는 반드시 로케이션헤더 있어야.자료위치 알려줌
- Accept 
어셉트 해더에게 html주세요~ 하고 보내야 서버가 정확히 알아요. rest api쓸때 같은 자료라도 어떤 형태의 자료인가 알아야 할때 (xml인지 json인지) 
- content-type
내가 요청하는거json 포함이야~혹은 클라이언트에게 알려주기위해 응답에 넣기도

## Content negotiation
네고시에이션, 서버가 어셉트 해더를 보고 json응답을 보내면 되겠군 하고 클라이언트에게 맞는형태의 자료를 보냄 


# Express 실습 
간단한 웹서버 구성

### 실습1 : .env에 name값 입력해보기 
<https://glitch.com/edit/#!/yoyocheckit?path=README.md:1:0>

> glitch 글리치 

: 웹브라우저에서 노드제이에스 코딩 가능
: 서버코드가 수정될때마다 자동으로 서버 재시작해줘서 편리
: 트렐로회사, 가끔불안정하면 새로고침 
: 깃헙 export됨 
: switch project 누르면 작업리스트 나옴 , 
: 제목이 url

- package.js
"scripts" : start 입력= node server.js
"dependencies" : 쓰는모듈  
- .env 
이 파일에서 환경변수 설정, 내용은 소유자와 공동작업자밖에 볼 수 없음

## Express
- node에서 가장많이쓰는 웹프레임워크
- 미들웨어(추가기능) 주입방식
- 공식메뉴얼 번역본 <https://expressjs.com/ko/> api참조부분 번역안되있지만 보기 

## Express 앱의 기본구조

~~~
// Express 인스턴스 생성
const app = express()

// 미들웨어 주입
app.use(sessionMiddleware())
app.use(authenticationMiddleware())

// 라우트 핸들러 등록
app.get('/', (request, response) => {
  response.send('Hello express!')
})

// 서버 구동
app.listen(3000, () => {
  console.log('Example app listening on port 3000!')
})
~~~
- 대부분 이 구조 
- 미들웨어 쓰는것만으로 추가기능 
- 라우터핸들러, 어떤 경로로 요청이 왔을때 특히 get요청  
라우터핸들어로 서버 짜기 (헬로우엑스프레스로 응답을 보내라)
- 서버켜기 app.listen 너의요청을 듣고있어, 성공하면 출력 


## Routing
- HTTP 요청 메소드(GET, POST, ...)와 같은 이름의 메소드를 사용
- app.get , app.post 알아보기 쉽게 짜여짐
- 라우트핸들러 (req, res) 관례로줄여씀 
- 첫번째 인자 :어느경로로 요청이 들어와 있는지
- 두번째 : 응답객체
~~~
app.get('/articles', (req, res) => {
  res.send('Hello Routing!')  //html보내고싶음 문자열
})
~~~


app.use(bodyParserMiddleware()) 이거랑 같은데 특정경로에만 주입 
~~~
app.post('/articles', bodyParserMiddleware(), (req, res) => {
  database.articles.create(req.body)
    .then(() => {
      res.send({ok: true}) //json으로 보내고싶음
    })
})
~~~

경로의 특정 부분을 함수의 인자처럼 입력받을 수 있음
콜론:id
~~~
app.get('/articles/:id', (req, res) => {
  database.articles.find(req.params.id) // `req.params`에 저장됨
    .then(article => {
      res.send(article)
    })
})
~~~
database의 articles에서 id와 일치되는 애를 찾아서 json응답을 보내도록짜여짐


## Request 객체
- req.body
: 요청바디를 js객체로 변환 이곳에 저장.    
익스프레스 기본내장에서 빠져서 body-parser 미들웨어 추가 기능 넣어야 
- req.ip
: 요청한 쪽의 ip
- req.params
: 파람스, 라우트 파라미터  
- req.query
: 쿼리스트링이 객체로 저장 {이름:값} 같은 정보들 

## Respons 객체
응답을 어떻게 보낼것인가
- res.status(...)
: 응답의 상태코드(200,300,400)를 지정 메소드 
- res.append(...)
: 응답에 헤더 추가
- res.send(...)
: 응답의 바디를 지정하는 메소드.  
텍스트면 html, 객체면 json로 응답


## 실습2 
<https://glitch.com/edit/#!/express-test1?path=server.js:27:0> 문제설명 
<https://glitch.com/edit/#!/wpsn-express-prac> 정답 

4.x API 설명<https://expressjs.com/ko/4x/api.html>

## Template language
탬플릿 작성할때 쓰는 언어 
php,jsp

## Template Engine
탬플릿과 데이터를 결합해 문서를 생성하는 프로그램 
html문서안에 코드를 집어넣는것들 , 템플릿엔진

# ejs
많이쓰는 템플릿엔진 (또다른것 jade, 아래참조 )
뷰파일내 자바스크립트 코드 그대로 사용가능   
문법단순  <% %>
엔진을 통해서 html 문법으로 변환
<http://ejs.co/>
vscode에 확장프로그램 : .ejs설치

~~~
<%# index.ejs %>
<html>
  <head>
    <title><%= title %></title>
  </head>
  <body>
    <div class="message">
      <%= message %>
    </div>
    <% if (showSecret) { %>
      <div>my secret</div>
    <% } %>
  </body>
</html>
~~~

설치 
~~~
$ npm install --save ejs
~~~

template engine 설정
~~~
app.set('view engine', 'ejs')
~~~

### 실습3 : 데이터와 ejs연결 
<https://glitch.com/edit/#!/wistful-suit?path=README.md:1:0>

- views/index.ejs : 별다른 설정없으면 views안에 
- res.render('index.ejs', data) 렌더함수, 응답보내는 메서드 
- index.ejs 빨강마크는 글리터가 아직 지원안해서 그럼
- <!--html주석은 삭제안되니까--> <% %>쓰기


### 실습4 : ejs파일 만들어서 프로필리스트 만들기 
<https://glitch.com/edit/#!/wpsn-ejs-prac?path=README.md:1:0>
<https://glitch.com/edit/#!/ten-layer?path=server.js:36:2>


.map()
.find()
.filter()

## html조합 시점 
- dom api를 쓸때는 클라이언트측 자바스크립트엔진만 가지고 사이트 만들었는데,
돔조작은 html와 js파일 불러와서 로딩끝난후 화면에 조작해뿌림. 서버1도없어  

- 오늘한건 주소를 치면 http요청이 서버에 날아가. 요청을 처리하는 핸들러들이 디비에 저장되 있던 프로필을  합쳐서 html문서를 만들어내어 서버에서 보내고 로딩이 완료되면 문서가 보여짐. 편집되는 시점의 차이 

- 데이터를 ajax를 통해서 불러와서 리액트 탬플릿과 함쳐서 클라이언트에서 조합 보여지는것


## pug 
상표권문제로 jade에서 퍽으로 이름변경   
고성능 템플릿 엔진이며 node를 위해 자바스크립트로 구현  
코드읽기쉬움, 닫는태그없는대신 들여쓰기 강제 (들여쓰기 안하는 개발자랑 협업할때 코딩스타일 강제해서 좋을듯) 
express사이트 탬플릿엔진 셋팅도 기본예제 pug


### 세미콜론 
body-parsers (익스프레스 미들웨어중 가장많이 쓰이는 라이브러리 )에서도 안씀   
자바스크립트 해석기는 앞뒤문장을 붙였을때 말이될경우 세미콜론이 자동삽입되지 않는다. 따라서 특수문자가 시작되는 곳에는 꼭 쓸것.
손가락 건강을 위해 좋은키보드와 세미콜론 사용을 줄이자.

<br>

※ 강사님 슬라이드  
<https://seungha-kim.github.io/wpsn-handout/>

