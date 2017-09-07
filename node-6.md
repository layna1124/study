# Cache

- 접근속도 개선을 위한 데이터를 복사한 임시저장하는 행위 
- http에서만 쓰이는게 아니라 네트워크, 데이터베이스,웹 등 많은분야 사용 

## HTTP Cache
- 웹표준 기술
- 서버에서 사져온 자원(html,css,js,이미지)을 가까운 곳(브라우저, 혹은 서버)에 저장하고 재사용 
- 캐시된 자원과 실제 자원의 내용이 달라지는 문제를 어떻게 해결할 것인가?

## Solution
1. 만료 : 정해진 시간지나면 캐시 자동으로 삭제, 속도가 중요한 css등의 파일
2. 검증 : (get 요청해서 api에서 받는자료 같은경우 복사본과 원본이 같아야 하므로) 캐시를 계속 사용할수 있는지 서버에 요청을 보내서  확인  

## Cache 관련 헤더들 
http해더들을 이용하여 캐시설저 

1. Cache-Control :  
(요청, 응답) 캐시와 관련 기능 지시자. no-cache, max-age(만료시간 등)
2. ETag :   
(응답) 캐시의 검증위한 식별자. 해시값, 마지막 수정시각, 버전 넘버
3. Expires : 익스파이어스   
(응답) 캐시를 만료시킬 시각을 서버에서 지정
4. Last-Modified :  
(응답) 원래 자료가 마지막으로 수정된 시각  
해당 시각 이후에 자료 수정됫으면 새자료 요청 등에 사용  
5. If-None-Match
(요청) 검증. 브라우저가 갖고잇는 식별자와 서버가 갖고있는 식별자를 비교하고 자료 전송여부 결정.     
이전에 저장해두었던 자원의 ETag 값을 If-None-Match 헤더의 값으로 요청에 포함시켜서 보내면, 서버는 해당 경로에 있는 자원의 ETag와 비교해보고 자원의 전송 여부를 결정
6. If-Modified-Since
(요청) 검증. 이전에 저장해두었던 자원의 Last-Modified 값을 If-Modified-Since 헤더의 값으로 요청에 포함시켜서 보내면, 서버는 해당 경로에 있는 자원의 Last-Modified와 비교해보고 자원의 전송 여부를 결정


## 개발자도구 확인 
<https://wpsn-axios-example.glitch.me/>
f12 - 네트워크 필터all
304코드 : not modified 변경되지안음  
1. wpsn-axios-example.glitch.me
Request header에 if-none-match:W/"bd4-15e54ec558e" 전에받았던 파일의 식별자가 저장된것을 확인  
위의 respone header에 etag:W/"bd4-15e54ec558e" 와같은것을 확인  
식별자가 같음으로 브라우저와 서버가 변경되지 안은것을 알수있음  
그래서 304응답을 보냄 (통신이 이뤄지긴 하는데 html 파일이 왔다갔다 하지안음)  
따로 설정 안했는데 304로잘 돌아감.

2. axios.min.js
검증되지 안은 axios 파일 쓰고있음 200 코드 
response headers 의 응답은 지금요청보내고 받은게 아니라 예전에 저장된것, 캐시에서 가져옴 
expires:Sun, 26 Aug 2018 02:12:20 GMT 까지 유효기간 
버전업데이트 되면 url이 바뀔것. 정보는 절대 바뀌지안을꺼라는 확신이 있으므로 저장기간 길어 

### 캐시삭제 
- [c]+[s]+r : 200코드뜸  (캐시가 되고있으면 304))
- f12 network - 브라우저 disable cache 체크하면 캐시남지안음 

## Cacheable Methods
POST 메소드는 Cacheable 범주에 포함되기는 하지만, 특별한 조건을 만족시켜야 하며 실무에서는 POST chace가 거의 사용되지 않습니다.

## 캐시의 사용
브라우저는 이미 캐시를 잘 활용하도록 만들어져 있습니다. Express도  
동작하지 않을 때 원인 파악위한 관련 헤더는 숙지. HTTP method를 용도에 맞게 


<hr>

# GraphQL
- 2015년 Facebook 데이터 질의 언어, REST API대체위해 
- 데이터의 구조를 GraphQL 언어로 정의한 후 질의, 서버는 그에 맞게 구조화된 데이터를 응답
- 서버에서는 GraphQL 질의용 해석기 필요, 어떤 언어나 개발가능 


### REST API 단점 
-  직관적으로 보여서 편해보이지만 각각의 자원마다 경로가 따로있어서, 한번에 불러오고 싶을때 요청을 여러번 보내야함 비효율적. 1자원=1경로 묶여져 
- 일부 속성만 필요해도 전체 가져와야

## 실습1 : GitHub GraphQL API
<https://developer.github.com/v4/explorer/>
깃로그인
우측 Docs에서 쿼리 찾아보기 
~~~
query { ㅗ
  user(login:"layna1124"){
    createdAt
  }
}
...
{
  user(login: "layna1124") {
    createdAt,
    repositories(first:20){
      nodes{
        name
      }
    }
  }
}
~~~
좌측박스안의 내용: 이 문자열을 통째로 서버에 보내면,   
서버는 우측박스안의 josn 데이터를 주는것  

그래프큐엘은 react와 엮어쓸수있는 릴레이가 유명세  
rest api쓰던 회사는 다바꿀수없으니 안쓸것 


<hr>


# SPA

ejs 서버측 탬플릿 언어지만 클라이언트측에서도 사용가능 

### 전통적 웹개발 
ejs통한 전통적인웹개발은 게시글 하나 추가하려면 통째 html다시 받아야함.
ejs를 통해서 데이터를 합친 결과물 html을 서버가 주면 웹브라우저가 보여줌.
그런데 form post를 하게되면  리다이렉트를 한번 시키고. 리다이렉트 경로로 한번더보내서 html새로 받아오고 새로고침.

## Single page Application
처음엔 html,css,js받아와.
필요요청 ajax로 보내. 서버가 잘 추가했어~ 라고 json으로 보내주고. 페이지는 리로드없이 필요부분만 업그레이드


## 실습2 : spa 초기방식 할일목록 리스트 
<https://github.com/seungha-kim/simple-todo-spa>
- fork : 저장소복사 (내꺼로), 포크한 저장소를 clone하기 : $ git clone [저장소 주소], 노드모듈스 폴더를 복원 : $ npm install, $ npm start

- 이번주에 공부한 innerhtml로 dom api 직접 사용방식이 아닌 
탬플릿엔진(ejs) 클라이언트에서 데이터만 주고받고 렌더링은 js엔진에서.

- 구조 : public > templetes > todos.ejs 이파일을 js엔진이 요청해서 ejs파일 가져옴. 할일목록데이터(배열)을 json형식으로 가져와서 브라우저쪽 엔진에서 합친뒤에 화면업데이트 

- 체크박스 : 체인지이벤트 이벤트리스너 
- (./data)데이터부분  
- form에 action없음, js측에서 form의 정보를 뽑아서 ajax요청하므로 
- index.js : (function (window, document) { //실제화면동작js

- 서버에서 할일 템플릿과 할일 데이터를 가져온 후, #todos 요소 안에 렌더링하는 함수
- function loadTodos() 화면을 다시 그려주는 함수 
- e.preventDefault() 기본동작취소, form은 전송이라는 기본동작(action도안썼지만 에러나니까), a태그 페이지 링크 
- e.stopPropagation() 이벤트버불링멈춤 
- 캡처 (Capture) / 버블 (Bubble) <http://blog.javarouka.me/2011/12/html-event-bubbling.html>
- e.target(이벤트 발생시킨것)보다 e.currentTarget 사용  
- 할일요청을 날려야 하는데, 필드에서 가져와야 form.elements사용, input name="title" 가져올수있어. name속성 title. 이런api가 있음  


- dataset: ~.dataset.id //데이타로 시작되는 모든속성 , 문자열 1.2 (우리가읽기엔 숫자지만 브라우저는 모름)
- 설정 loadTodos() //화면 통째다시그려주기, 개발하기에 탬플릿이 편하긴 한데 리액트가 필요한것만 골라서 그려줌.  
- node.js로 서버 만들기는 리엑트보단 쉽지만 서버개발자가 여러서버에 배포관리하기에는 
- react 쓰면 webpack을 써야하는데, (function (window, document) { }) 이런것도 안해도됨

- 이전 익명게시판과 다른점 렌더링안함. render를 쓰는부분이 없어. json응답 혹은 빈 응답을 하고있음, 심지어 post, delete, 도  redirect 필요없고
ajax요청은 사용자가 새로고침 할수없으니까 리다이렉트 하지 안아도 안전. send end만 있어.
- 서버가 로컬호스트 접근시 정적파일 중 index.html을 대신보냄

[과제 추가기능]
- title 수정 기능
- '기한'
- 디자인 개선
- 로그인

---

- 크롬에서 네트워크 속도 느리게 만들기 Slow, GPPS offline도 가능 
- 낙관적업데이트 (다수) / 비관적업데이트 
- 크롬 디버깅 / node 디버깅


 