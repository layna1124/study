### 목차 
- Ajax : ajax요청 보내는 실습  Axios엑시오스 이용 
- CORS : Cross-Origin Resource Sharing, 다른도메인 HTTP 접근 제어 
- JWT : json Web Token, 쿠키말고 토큰형식 인증방식
- Fetch API : ajax를 보내는 웹브라우저용 api


# Ajax
- 비동기적인 웹어플리케이션 제작을 위한 클라이언트 측웹개발 기법 (지난시간까지 한건 자바스크립트를 안쓰는 전통적인 웹개발 기법)...을 뜻했으나 현재는 
- 웹 브라우저에서 XMLHttpRequest 혹은 fetch를 이용해서 보내는 HTTP 요청을 통칭

## Ajax model
![](https://blog.spec-india.com/wp-content/uploads/Traditional-Web-Application-Model.jpg)

## Ajax 장점
- 화면전체 재로드 안하고 갱신가능
- 서버응답 기다리는 동안 웹어플리케이션 사용가능
- 필요자원만 서버에서 받아서 트래픽 줄어듬

## 단점 
- 클라이언트 구현이 굉~장히 복잡해짐 
- 서버에서도 데이터처리를 해야하고 클라이언트에서도 데이터처리를 해야하고 dom api도 다뤄야해서, jquery로 하다가 angular, Vue, react 등이 등장


## 라이브러리
- isomorphic-fetch, superagent(콜백기반), axios 많이 사용, 브라우저와 Node.js에서 모두 사용  
- jQuery, xmlHttpRequest

## Axios
- Promise based HTTP client 최근인기 
- 브라우저와 Node.js에서 모두 사용가능
- XMLHttpRequest, fetch보다 쉽고 기능많음
- 브라우저에서 사용하면 XMLHttpRequest를 사용하여 Ajax 요청을 보내고, 
- Node.js에서 사용하면 내장 http 모듈을 이용해 요청을 보냅니다. 
- 사용법 간단하며 Promise 기반으로 코드깔끔 


## 실습1 : Axios + json-server  
<https://ajax-axios.glitch.me/>
- db.js파일 만들고, show에 나온 페이지에 명령어, 브라우저 콘솔에 하나씩 넣어서 확인하기

- json-server 패키지를 사용해 REST API를 제공. json-server는 내부적으로 express를 사용하고 있어서 커맨드라인을 통해서 json-server를 실행시키지 않고 직접 자바스크립트 파일에서 불러와 사용할 수 있다.

- npm사이트에서 보기 config사용 

- rest api와 통신할때 우리가 쓰게되는 5가지
- post 자료생성, get 자료읽기, put 통째치환, patch 요청부분만 갱신, delete 

- promise 계속사용, 이해하고 넘어가기 


## 실습 2: 쿠키를 통한 (로그인)인증예제 
<https://glitch.com/edit/#!/axios-cookie?path=server.js:43:37>
- 어제실습 form으로 username pw 날렸는데 bodyparser urlencored 필요했는데 
- 오늘은 json으로 
- 로그인을 해야 json서버 사용할수있게 설정 

- 성공실패 표시 예제찾아보기 

- ajax갖고 쿠키를 사용할수 있다
- set-cookie 응답 , 정보를 브라우저

<hr>

### 문자열 --> 정수
(1) parseInt: 파즈인트를 쓰자. 
  ~~~
  try{
   parseInt()
  }catch
  ~~~  

(2) *1 : 비추  왜?  
: undefined에 *1 하면 NaN이 나오는데  
if(result === NaN){} 이렇게 비교하면안되 있어도없어도 항상 false야. js에서 자기자신값과 다른게 딱하나 있는데 NaN임, NaN === NaN //false 임 ! 헐...  
새로생긴것도 있긴함 (Number.inNaN)

사용자 NaN막 뜨면 고객센터 전화하고 ㅋㅋ 
에러가 나야하는 상황에서는 에러를 내주는게 좋다 

<hr>

## same-origin policy  
- 웹페이지에서 리소스를 불러올때, 출처(=프로토콜 + 도메인 + 포트번호)가 다르면 (3개 같아서 동일출처임) 안전하지 않다고 웹브라우저가 각종 보안을 작동시킴.
- 보내는쪽과 받는쪽이 다를때 생기는 문제 
- 프로젝트할때 프론틀아 백이랑 다른서버 올렸다가 합치려고 햐면 문제싱길것 

### 해보기  
~~~
//기존창
> foo = 'bar'
"bar"
> window.open('http://www.fastcampus.co.kr') 
//새로열린 창에서
> window.opener 
//기존창의 것이 참조가됨 
> window.opener.foo
"bar"
//기존창에서 
> const child = window.open('http://www.fastcampus.co.kr')
// 새로 열린 웹 페이지의 콘솔에서
> window.foo2 = 'bar2'
// 이전 웹 페이지의 콘솔에서
> child.foo2
// 출처가 같다면 접근 가능, 아니면 불가
~~~


# CORS
- Cross-Origin Resource Sharing
- 클라이언트 측 cross-origin 요청을 안전하게 보내는 방법 표준
- 스크립트가 출처가 다른 API 서버를 사용하려면 추가적 처리 필요!


## Cross-origin 요청의 위험성
- mywebsite.com에서 서비스 중인 웹 사이트는 mywebsite.com/api 에서 REST API를 통해 필요한 정보를 얻습니다. mywebsite.com/api 경로에 대한 인증은 쿠키로 이루어지고 있습니다.
그런데 만약 evil.com 웹 사이트의 스크립트에서 mywebsite.com API에 요청을 마음대로 보낼 수 있다면, 이미 my-website.com 도메인에 대해 브라우저에 저장된 쿠키를 이용해서 API를 마음대로 호출할 수 있을 것입니다.

- IE8 이상 cross-origin 요청에 제한둠.
- cross-origin 요청 허용하려면, 서버가 특별형태의 응답 전송해야
- 만약 서버가 cross-origin 요청을 허용하지 않으면, 에러를 발생시킴



## 실습3 : Cross-origin 요청 예제
<https://glitch.com/edit/#!/cross-origin>

- 응답이 와도 브라우저가 버림 
- 최근의 브라우저는 개인정보많은 플랫폼이 되어서 공식버전 사용을 권장한다.


## CORS에 관여하는 응답 헤더
* Access-Control-Allow-Origin
* Access-Control-Expose-Headers
* Access-Control-Max-Age
* Access-Control-Allow-Credentials
* Access-Control-Allow-Methods
* Access-Control-Allow-Headers

## CORS에 관여하는 요청 헤더
* Origin  
* Access-Control-Request-Method (preflighted 전용)  
* Access-Control-Request-Headers (preflighted 전용)  


### 프로젝트 할때 cors설치해도 쿠키가 포함 안되요. 
: cross-origin 요청에는 기본적으로 쿠키가 포함되지 않는다!  
XMLHttpRequest 혹은 fetch를 통해 요청보낼때 옵션으로 가능하나 보안조건 엄격해짐 


### 복잡하면 그냥...
1. 프론트엔드와 API 서버를 같은 도메인으로 제공한다.
2. 불가피하게 둘을 다른 도메인으로 제공해야 한다면
  2-1. CORS를 허용한다 (cors 미들웨어를 사용하면 간단함)
  2-2. CORS를 허용했으므로 쿠키를 쓰지 않는다.


## 쿠키를 안 쓰면 어떻게 인증을 하죠?
Access Token & JWT, 토큰기반인증 


## Cookie인증 vs Token인증
(1) Cookie-based Auth :   
서버측 탬플릿 언어를 사용하는 방식, set쿠키해더포함, 쿠키인증 사용  302, 브라우저가 정보를 기억  
쿠키를 지원하는 클라이언트에서밖에 사용할 수 없음, 보안에 취약하며, CORS 대응이 복잡함.  
쿠키가 웹브라우저에서만 동작하므로 모바일웹같은 트렐로(서버랑 통신할때) 쿠키를 쓰기가 그래서 다른 인증방식을 개발. 토큰형식(아이디 패스워드 대신 사용하는 jwt)



(2) Token-based Auth :   
- json으로 내가 토큰발급해줄께 200, 우리가 짠 클라이언트측 자바스크립트가 정보를 기억     
- 요즘트렌드, 모바일웹도 같이 사용하는 일이 많아져서
- 토큰이란, 사용자의 아이디, 패스워드 등을 통해 인증후, 특정 자원에 대한 인증 수단. 서버에 요청을 할 때마다 토큰을 요청에 직접 포함시켜서 전송 (주로 Authorization 헤더에 넣어서 전송)
f12 > Headers > Request headers > Authorization: Bearer (토큰~
사람이 알아볼수없는 긴 문자열)
- 암호화 사용자가 많으면 CPU가 암호해석에만 매달려야 해서 서명을 활용



## 토큰 장점
- 다양한 인증 수단(전화번호, 공인인증서, 생체정보 등)의 인증 결과를 토큰이라는 하나의 수단으로 통일
- 쿠키를 사용하지 않으니 CORS문제 회피

## 토큰 단점
- 매 요청에 포함되므로 적당히 짧은 길이
- 유출에 대한 대비책(토큰에 유효기간, 유출된 토큰을 강제로 무효화 등)
- 쿠키와는 다르게, 클라이언트에서 우리가 직접 토큰을 저장하고 관리

## Web Storage
- 브라우저에서 키-값 쌍을 저장할 수 있는 저장소
- 쿠키에 비해 편리하고 용량큼(10MB 가량)
- 브라우저 탭이 닫히면 내용이 삭제되는 sessionStorage, 브라우저 탭이 닫혀도 내용이 유지되는 localStrage
- localStrage이용시 .setitem  .getitem으로 조작해주세요.  

## 보안상 주의 
- localStrage 이용시 토큰을 탈취당할수 있어서 xss(크로스사이트스크립팅)에 신경쓰라고 하는데 직접 dom api에 innerHTML는 실무에서 절대 사용하지 않는다.
- EJS, REACT, PUGM VUE 같은 탬플릿엔진에는 방어수단이 다 들어있다.

<hr>

# JWT
JSON Web Token 
- 최근인기 토큰형식의 표준
- 토큰 안에 JSON 형식으로 정보를 저장
- 서명 혹은 암호화를 통한 보안 
<https://jwt.io/>



## 실습4 : jwt 
<https://glitch.com/edit/#!/jsonwebtoken?path=server.js:118:0>
- server.js 읽어보기
- <https://jsonwebtoken.glitch.me/>에서 실험 
- express 및 다른 패키지들을 이용해 JWT를 통한 인증을 하는 서버를 구현
- Postman과 JWT를 이용한 API 사용
- Axios와 JWT를 이용한 API 사용
- 요청 보낼때마다 token을 포함시켜야
- 중복제거하려면 Axios라이브러리의 instance 사용 
- Authorization 해더에 자동포함 날아감 
~~~
// Axios.create
const authedAxios = axios.create({
  headers: {
    'Authorization': `Bearer ${token}`
  }
})
authedAxios.get('/auth').then(res => {
  prettyPrint(res.data)
})
authedAxios.get('/some-api').then(res => {
  prettyPrint(res.data)
})
authedAxios.post('/count').then(res => {
  prettyPrint(res.data)
})
~~~

# Fetch API
- 웹 브라우저의 XMLHttpRequest를 대체하기 위해 만들어진 새로운 HTTP client 표준.  
- XHR 는 그렇게 좋은 API는 아니였음 
- Fetch API 는 HTTP 프로토콜의 모든 개념을 JS 에 똑같이 도입
- 구형 브라우저지원 안함
- <http://hacks.mozilla.or.kr/2015/05/this-api-is-so-fetching/>


## Axios vs Fetch API 
- Instance와 같이 설정을 재사용하거나 요청중인 연결을 취소하는 등의 편의기능이 Fetch API에는 없음
현재로서는 Axios를 사용하는 것이 좋은 선택
- axios가 내부적으로 xmlhttpRequest를 사용하므로, Service Worker 등의 웹 최신 기술이 XMLHttpRequest를 지원하지 않으니 이땐 사용할수없다.




<hr>
[검색]

- promise 공부 <http://programmingsummaries.tistory.com/325>
- 리액트 고수들 커뮤니티 gitter <https://gitter.im/reactkr/discuss>
- http접근제어 <https://developer.mozilla.org/ko/docs/Web/HTTP/Access_control_CORS>