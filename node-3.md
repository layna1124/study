# HTML form
입력정보가 퍼센트인코딩 되어 전송

> get method
~~~
GET /search?query=%EA%B0%9C&sort=latest HTTP/1.1
~~~
?쿼리파라미터=이름은값 (한글이면퍼센트인코딩) &
겟은 리퀘스트에 포함되어 가는데 

> POST methode

포스트로 폼을 전송할때 
content-type 이 자동셋팅되어 전송
아무설정도 하지안으면 url인코딩도 방식으로 전송
파일을 전송할수가 없어..해결위해 다른 컨텐트타입이 있는데 다음장 
~~~
POST /form HTTP/1.1
Content-Type: application/x-www-form-urlencoded
...

home=Cosby&favorite+flavor=flies
~~~

## multipart/form-data
- 기본 설정(percent encoding)으로는 폼으로 파일을 업로드하는 것은 불가능
- (클라이언트 측) form 태그에 enctype="multipart/form-data" 속성을 적용하면 파일 업로드 가능
- (서버 측) body-parser 미들웨어는 multipart/form-data 형태의 요청을 지원하지 않음 (보통 폼을통해 파일업로드를 하지않기때문에 바디파써만 쓰는것이일반적 , 혹시 파일업로드 처리 필요시 멀터이용 multer <https://www.npmjs.com/package/multer>)

## 응답확인하기 
개발자도구 - 네트워크 선택 
- preserve log 체크박스선택 (원래했던 요청 기록남아, 리다이렉트 확인할때)
- disable cache
익스프레스 기본 302응답 
http니까 요청보내면 응답이 옴.상태확인 (지금 배열기반 새로고침 누르면 리스트 다 지워져)
301로 리다이렉트 보내면, 웹브라우저가 서버에 요청안하고 웹브라우저에 있는 기능을 갖다씀 : 원래 웹사이트 주소가 폐쇠되고 완전히 이동했을때, 캐시 


## 실습1 : 할일리스트 todo form
<https://glitch.com/edit/#!/0829todo?path=views/index.ejs:1:0>


### Form validation
사용자에게 입력받은 자료는 개발자 기대와 다를수있어 그대로 입력받으면 데이터베이스가 엉망이 되믈, 처리를 하기 전에 항상 올바른 형태인지 검증이 필요
(1) 서버측 벨리데이션 : 서버는 데이터가 기대한 대로 잘 들어왔으면 다음 단계를 진행하고, 데이터에 문제가 있다면 어떤 문제가 있는지를 사용자에게 알려줍니다.
지금 404페이지같은 , 악의적인 해커가 Postman 등을 이용해 이상한 요청을 보낼 수 있으므로 클라이언트측 벨리데이션만 해서는 안됨. 
(2) 클라이언트측 벨리데이션 : 전송전 폼작성중에 잘못된 것을 알려줌.  
일일히 js로  input이 일어날때마다 js로 이벤트를 검사하고 form에 submit 할때 넣음

(2-1) html5 form validation
~~~
<input type="text" name="title" required > //입력안하고 전송누르면 메시지 
~~~
브라우저에 내장되어 있다는 점에서 (특히 모바일에서) 일관성있는 사용자 경험을 제공할 수 있다. 여러 필드의 자료를 합쳐서 validation을 한다거나, validation을 하기 위해 서버에 요청을 해야 하는건 지원 안한다.




### Redirect 
- 순수한 HTML form을 이용해 POST 메소드로 자료를 전송한 후에는 꼭 리디렉션을 통해 응답해야함. 특히 302 상태 코드
- 브라우저의 새로고침은 이전에 보냈던 요청을 똑같이 다시 보내는것 
- 사용자가 새로고침하면 똑같은 요청이 게속 가기때문에 리다이렉트를 시키는것  
- Ajax를 통해 자료를 전송하는 방식이라면 2xx 상태코드의 일반적인 응답을 해도 ehls다. 



## url 쇼트너
<https://goo.gl/>
개발자도구 preserve log 체크박스, other에서 301확인 
긴 url을 짧게, 사용자가 리다리렉트 시켜주는 서비스 


## 실습2 : 라이브코딩 개발 
글리치 서버로딩 느리니까 깃에 올림 
vscode로 expresss 사용시 수정마다 서버재시작 하기  


# 시나리오 설계 
### 관리자 url변환
1. 로그인 
2. 긴url을 폼에 입력하고 전송 
3. 서버에서 url변환
4. 결과확인
### 짧은 url이용
1. 방문자, 관리자가 짧은 url접속 
2. 서버는 301응답
3. 긴 url로 리다이렉트 됨
### url목록 열람 (관리자)
1. 로그인
2. 루트경로에서 열람 
## ui설계 
1. 로그인 : 브라우저기본
2. 목록 : 긴url / 짧은url (th)
(100개일때:pagenation, 없을때:)
## 데이터 설계
1. 큰배열에[ 객체로 {긴 url, 짧은 url} 객체로 여러개] , 객체분류 식별자 필요 
2. 긴url에 두개의 짧은 url을 넣을것인가, 이건 선택의문제



## git ignore 
깃 이그노어 확장프로그램 설치   
[f1에서 검색 add git - node 누르면 .gitgnore 파일생성]   
시작할때 설치하면 편함  
이러면 깃 저장소에 깃해도 node_modules는 안올라가  
(node_modules폴더는 우리는 express만 설치해도 연관된게 모두 설치)   
나중에 배포할때 package.json 받아서 클론받은 사용자가   
npm install하면 내가만든 그대로 노드모듈스가 설치된다.  

## git history 설치 
[f1에서 검색 git history 출력됨]  


## vs코드에서 git init
좌측 사이드에 있는 Git 메뉴버튼을 클릭,initialize버튼  
git init 하면 .git이 생김  
ls -al 숨긴파일보기 명령어 누르면 .git 이 보임


## vs코드에서 커밋하기 
- 좌측 소스제어버튼 
- U : 언스테이지상태 
- A : U에서 + 누르면 변경 하고 하나씩 커밋해서 변경 
- 설정따라 : 커밋만 누르면 unstaged된 상태를 전부 staged로 바뀌고  



--save하면 pakage.json에 기록도 되고 
~~~
$ npm install --save express
~~~

## server.js
~~~
const express = require('express')
const app = express()

app.get('/',(req,res) => {
  res.send('hello express')
})


app.listen(3000, () => { //listen해야 서버가 구동
  console.log('listening...')
})
~~~

## 브라우저 열기 
127.0,0,0.1:3000  
localhost:3000  



컴퓨터에서 서버실행시키기 
~~~
> node server.js
~~~
[c] + C : 서버종료

수정하면 다시 재시작해야함 (방향키 위로)
npm start 라고 설정하는것이 관례 
"start" : "node server.js" 추가하고
npm start로 입력 



server.js
~~~
//express가 자동으로 ejs를 불러와서 탬플릿엔진으로 사용할수있음
app.set('view engine', 'ejs')
~~~
views폴더 생성 - index.ejs 파일 


## ejs에서 에믹쓰기
~~~
"emmet.showExpandedAbbreviation": "always",
"emmet.includeLanguages": {
	"javascript": "html"
},
"emmet.triggerExpansionOnTab": true,
~~~



## 로그인 
npm사이트 express-basic-auth 검색
<https://www.npmjs.com/package/express-basic-auth> 첼린지 부분 
~~~
const basicAuth = require('express-basic-auth')
...
app.use(basicAuth({
  users: { 'admin': '1234' },
  challenge: true,
  realm: 'Imb4T3st4pp'
}))
~~~
css수정은 안됨 


## npm 랜덤문자열생성
<https://www.npmjs.com/package/randomstring> 
~~~
$ npm install --save randomstring
~~~


## 일렉트론 
데스크탑인데 웹브라우저처럼 동작 
학생성적표 파일1000개 클라우드에 올리고 학원원번_난수.html 
구글이랑 비틀리는 한번에 많은 url을 생성할수없어. 1시간에 100개정도밖에 안되서 구현함 




## 폼 바디파서
npm사이트 body-parser
Express/Connect top-level generic 선택
~~~
npm install --save body-paroser
~~~

~~~
const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({ extended: false }))
~~~


# 나우 
위에 만든것 내컴퓨터에서만 되기때문에 서버가 필요할때 
<now.sh>
~~~
$ npm install -g now 

$ now
~~~
이메일등록 하여 사용   
정말 배포할껀지 물음      
개인정보 포함하지않고 배포하는 방법 있는데 다음에..
실행 할때마다 url 계속바뀌므로 마지막 url로 주소올리기 
윈도우 안될수 


# 과제
- 익명게시판 : 누구가 글과 댓글 쓸수있음
- 관리자페이지 별도 : 글삭제 
  (글마다 각 항목마다 삭제하는 form을 따로만들기,돔쓰지않고 get과 post밖에 못쓰는 제약)
- now동작 안하면 깃에만
- 조교님 시트에 깃저장소 올리기
- 백엔드는 서버 재시작되도 삭제안되게 만들기 
- 서버사이드에서 라우터 (기존에 한건 싱글페이지는 데이타 api만 가져오는것)  


## npm start 자동재식작
노드모드 서버 돌아갈때 js수정저장할때마다 [c]+c 재시작 반복 안해도됨  
윈도우는 노드랑 궁합이 안맞아 안될수 있음
~~~
$ npm install --save nodemon 
~~~
추가
~~~
"scripts"{
  "dev" : "nodemon server.js"
}
~~~
~~~
$ dev 
~~~

강사님 슬라이드    
<https://seungha-kim.github.io/wpsn-handout/>
강사님 깃   
<https://github.com/seungha-kim/url-shortener-fastcampus/commits/master>