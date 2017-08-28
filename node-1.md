# Node.js

김승하 (4년차 웹개발자, 풀스택)
커리큘럼 
Node.js : 자바스크립트를 노드로 실행 
HTTP : 서버와 클라이언트 같이
JS : 최신기술쓰기위해 좀더

 0828 강의 슬라이드 https://seungha-kim.github.io/wpsn-handout/


## REST API실습 
깃헙이 제공하는 RESTAPI 사용해보기 
https://developer.github.com/v3/
rest api 비밀번호 필요한거 필요없는거 같이있음 

### users 카테고리 
<postman> get 에서 https://api.github.com/users/layna1124 입력해보기 
https://username:password@api.github.com/user 입력해보기 
안나올경우 Authorization type을 No Auth에서 basic auth 베이직어스 방식으로 인증하면 나옴


### Repositories 카테고리 
- 저장소 나열하기
get 에서 https://api.github.com/user/repos


## node최신설치 8.4

경로상관없음

윈도우경우
<https://github.com/coreybutler/nvm-windows>
Download the latest installer from the releases. 
<https://github.com/coreybutler/nvm-windows/releases>
nvm-setup.zip 다운설치 후 터미널재실행 
$ nvm install 8.4
$ nvm use 8.4
$ nvm alias default 8.4 (# nvm-windows는 필요없음)

npm install -g로 깔았던게 6.11.x버전으로 종속이됨
지금 8.4로 깔아서 이전꺼못씀.  
원래 깔았던 버전으로 돌아가기 
$ nvm ls  설치한목록뜸 (6.11.1)등 
$ nvm use 이전버전 


$ node
> 꺽쇠뒤에 자바스크립트 코드 입력
> .exit 나가기 

크롬개발자 도구가 보여서 편하긴한데 여기서도 쓸수있다는거

// Node.js module 사용하기
> const os = require('os') // 급할땐 `os = ...`

os라는 모듈을 불러와서 ..객체를 os에 넣는 = os모듁=os객체
그 기능을 사용할수있어
운영체제에 접근하거나, 서버만들거나, 파일에 접근가능

노드사이트 
<https://nodejs.org/dist/latest-v8.x/docs/api/>
쓸수있는 모듈 리스트 나옴 
os 모듈 내장모듈을 직접쓸일이 많지는 안으나 
path 모듈 가끔사용 

- 직접쓸일은 별로없고 만들어둔 js를 실행
$ node index.js



## Javascript Runtime
- js를 구동하기 위한 실행환경(각각의 환경)
- 프로그래머는 런타임이 제공하는 도구를 이용하여 프로그램개발
- 웹브라우저나 node.js도 자바스크립트런타임의 일종  
- 포토샵도 반복적인 업무 js로 짜서 실행하므로  포토샵도 
자바스크립트 런타임이라고 할수있음
- monggoDB, Chrome, Node.js 등등

## v8 js Engine
- v8js엔진 나오기 전에는 익스에서 js실행속도가 매우 느려서 적게사용함
- 크롬이 나오고 v8이 나오면서 웹이 풍부한 사용자 경험을 제공하는 플랫폼으로 발전
- 코드최적화 기능, 기계어로 변환

## Event-driven 프로그래밍 
- 프로그램 흐름(양식)
- 이벤트 드리븐의 좋은점 : 미리 정해진 이벤트에 미리 정해진 방식으로 이벤트 핸들러를 작성함으로써 외부이벤트가 일어났을때 코드를 사용
- 웹브라우저 처럼 사용자를 기다리거나 서버같은 요청응답을 기다리는 프로그램을 쓸때 사용 
- 노드js 에서는 매번 이벤트 핸들러를 입력하기 보다는 프레임워크를 사용

## Non-blocking 
- 스레드(프로그램)가 입출력 기다리지 않고 코드실행 
- 실제 실행속도가 뒤죽박죽 될수있어, 복잡한 코드
- node.js가 많이사용
- 반대어 blocking I/O  : io는 보통 입력기다릴때가 많기때문에 붙임


# Module

윈도우나 다큐먼트처럼 접근가능
~~~ 
module.exports =   //객체새로만들어서 집어넣을때

exports.add = //module. 생략가능
~~~
빈객체가 들어있음 
규칙싫으면 무조건 module.exports 익스포츠쓰기

# NPM
Node.js 패키지 관리 도구 + 클라우드 패키지 저장소
- 의존 패키지 관리
- 스크립트 실행
- 패키지 설정
- NPM에 패키지 배포
- Node.js 종합 작업 도구



## 작업
~~~
$ mkdir hello-npm
$ cd hello-npm
$ npm init -y   //pacage.json파일생성 
$ code .        //vs열림 
~~~
-y : yes라는뜻 
설정하혀면 안쓰고 만들면됨

## package.json
- dependncies : 디펜던씨   
npm install --save` 명령으로 설치한 패키지가 기록됨  

- scripts 
자주사용되는 명령어 짧게쓰기  

~~~
// index.js
const randomstring = require('randomstring')
console.log(randomstring.generate())
~~~



node_modules에 저장됨
~~~
$ npm install --save randomstring 
~~~

자주쓰는 명령어 추가 
~~~
// package.json
...
  "scripts": {
    "start": "node index.js" //추가
  }
...
$ npm start  //node index.js 터미널에 쓴것과 동일하게 실행됨 
~~~

## Concurrency Model
동시성모델 
- 클릭하고 요청하여 표시되는 과정:생애주기와, 
github이 슬랙에 요청을 보내고 받는:생애주기가  
동시에 일어나 같은 컴퓨터의 자원,리소스의 사용이 겹칠 경우 어떻게 충돌이 생기지 않게 할것인가?
- 자바스크립트는 이러한 충돌을 염려할 필요가 없다

## resource
- cpu : 계산은 cpu로 하는건데 cpu의 개수는 제한되어 있어.
cpu를 공유해야 할일이 생기고
- 메모리 : 에 저장된 자원
- 네트워크 

## thread
- 쓰레드란 코드를 실행하는 작은 (논리적)기계
- 프로그램 안에 여러개 
- 개념은 cpu가 사용, cpu코어하나는 하나의 스레드 실행
- 자바스크립트를 실행시키는 스레드는 하나뿐 작성이 쉬움 
- 실행과정(콜랙연쇄)의 실행주기가 겹칠수있지만 동시에 실행되는 경우는 없음
- 메시지큐(쌓여있다가 자동으로 처리)를 활용 


- cpu를 많이쓰는 작업에 부적절
- 오래걸리는 js코드가 하나의 스레드를 독점하고 있으면 전체에 영향
: 외부(db, node,browser)에 위임하기, sass가 node에서 컴파일되서 넘기는것처럼  
: 여러개의 함수(메시지)로 쪼개기, 다른실행과정(사용자에게 보여줘야할)이 끼어들 틈을 주기


# 비동기 자바스크립트
Asynchronous Callback
- "나중에 실행해줘" = 비동기  코드작성법은? 
- 함수를 호출할때, 콜백까지 같이 인자에 넣기
- 모든 콜백이 비동기는 아님 "지금 바로해줘"라는 콜백도 있음 ex).msp

## readFile : 
node.js함수
"나는 계속 갈테니 파일읽는게 완료되면 알려줘"
첫번째인자 에러
두번째인자 부터 데이터를 받음
~~~
const fs = require('fs') // Node.js 내장 모듈
fs.readFile('./calc.js', 'utf8', (err, data) => {
  console.log(data)
})
console.log('done!')
~~~
done! 부터 출력 
파일이 완료되면 (data)출력

~~~
const fs = require('fs') // Node.js 내장 모듈
const data = fs.readFileSync('./calc.js', 'utf8')
console.log(data)
console.log('done!')
~~~
위 경우 당연히 data부터 출력

~~~
const fs = require('fs') // Node.js 내장 모듈
fs.readFile('./calc.js', 'utf8', (err, data) => {
  if(err){
    console.error(err)
  }else{
    console.data(data) //에러가없으면 데이터를 출력 
  }
})
console.log('done!')
~~~
try{}catch(e){} : 동기식처리에서씀 

자바스크립트 표준 ;자동생성 안써도 되는데 
(), []시작문구는 ;()  , ;[]로 써주기 

# request설치
후에 다른것으로 바꿔쓸 에정  

~~~
$ npm install --save request
~~~ 
5.부터는 --save안써도 되 

Github REST API 호출하기 
~~~
// 유저 이름, 저장소, 나에게 할당된 이슈 갯수 출력하기
const request = require('request')  //reauest불러오기위해 require함수
const apiUrl = 'https://api.github.com'  //
const option = { //request를 쓰려면 이런옵션 써야해 
  json: true,
  auth: {
    'user': 'username', //본인 
    'pass': 'password',
  },
  headers: {
    'User-Agent': 'request'
  }
}
// 요청보내고싶은  첫번째 깃헙 url 요청  
// 첫번째 error관습, 두번째인자 콜백, 세번째 body에 진짜 정보들어있음  
request.get(`${apiUrl}/user`, option, function (error, response, body) {
  const name = body.name  //body안에 name참조 변수 name으로저장 
  if (error) console.error(error)
  // 콜백 안에 콜백
  request.get(`${apiUrl}/user/repos`, option, function (error, response, body) {
    if (error) console.error(error)
    // 문서보면 배열로 반환하고있어. 안에 요소 객체 
    const repoNames = body.map(item => item.name)
    // 콜백 안에 콜백 안에 콜백
    request.get(`${apiUrl}/issues`, option, function (error, response, body) {
      if (error) console.error(error)
      const issueNum = body.length
      console.log(`name: ${name}`)
      console.log('repos:')
      repoNames.forEach(name => {
        console.log(name)
      })
      console.log(`num of assigned issues: ${issueNum}`)
    })
  })
})
~~~
콜백안에 콜백 콜백..들여쓰기의 연속..이런 복잡한 코드밖에 만들수없음  

# Promise
- 위의 문제를 해결하기 위해 js에서도 비동기 코드를 깔끔히 짜보자 해서 나옴   
- 라이브러리 형태: npm 블루버드 <https://www.npmjs.com/package/bluebird>  
  es6를 쓰면프로미스가 내장되있음으로 쓸필요 없음
- 비동기 작업의 결과를 담는 객체
- 정확히 언제가 될지 모르지만, 결국 성공 또는 실패의 상태를 갖게 됨. 이 상태를 갖게됫을때 콜백을 실행


~~~
// tenSec.js
module.exports = function tenSec(value) { //value 라는객체 함수 
  return new Promise((resolve, reject) => { //프로미스 생성자는 함수를 받는데 인자두개
    setTimeout(() => {
      resolve(value)
    }, 10000)
  })
}
~~~
프로미스 객체를 새로 만들어서 반환함
1. 프로미스 결과담기  
2. 내가 프로미스가 성공실패 했는지 컨트롤 

new promise 
resolve라는 함수를 인자로 
두번째 reject라는 함수를 인자로 

비동기 작업을 실컷한후에 resolve로 넘김 
10초뒤에  tensec값으로 넘어온 value를 성공시켜라 

~~~
// REPL
> const tenSec = require('./tenSec')
> const p = tenSec(1) //1를 호출하면 p에 저장 
> p // 만든지 10초가 지나기 전
Promise {
  [pending],  //아직 성공.실패안나온 비동기연산 안나온상태
  ...
> p // 만든지 10초가 지난 후 펜딩사라지고 1나옴 
Promise {
  1,
  ...
~~~
tecSec 모듈을 불러와서 변수로 저장 , 객체든 문자든 함수든 상관없어 


# .then
- callback hell싫어 가독성 위해 사용
- 프로미스를 반환하는 함수(비동기코드 짜기쉽게)
- 새로만들어지는 코드들은 callback거의 안쓰고 프로미스를 사용

이미 끝난 이벤트에 대해서도 이벤트 실행
완료된 프로미스 p.then

~~~
 p.then( v => {
   console.log(v)
 })
 tenSec('hello promise').then(val => {
   console.log(val)
 })
  // 10초 후 등장 
 > 'hello promise'
~~~
then안에서 return된값을 품고있는 프로미스 객체가 반환됨

## promise chaining
~~~
// chaining.js
.then(value =>{
  return 2
}).then(value =>{
  return 3
}).then(계속 쓸수있어)
~~~
return은 콜백을 넘겨 값을받고 추가작업을 하잖아
then안에서 return tenSec(3) 프로미스를 리턴하면 3만 다음valuse로 넘어감 

- 프로미스함수 : promise.resolve(3)

pa = Promise.all([p1,p2]) 모든 프로미스를 성공하면 자기도 성공하는 프로미스 


- callback으로 하기 어려운일 지원하는 promise
- 비동기로 다 성공후 추가작업할때 

- node 비동기콜백 방식으로 되어있는데 node8버전부터 프로미스를 반환하는 함수가 될수있어 
util모듈에 require 

## Promise.all

- callback를 넘기징낳고 promise로 넘기는 라이브럴리


- ajax요청을 하는 여러 라이브러리  : 보통 프로미스 구현
ex) axios,

- 실무에서 T쓰는 정말멋진 Fetch API
- 

## Async/ Await
어싱크 어웨이트 
js표중네 포함됨
비동기식 코드를 동기식처럼 
널리도입 되지 안아서 promise쓰고 이거쓰지 안을예정 

~~~
const tenSec = require('./tenSec')

async function resolveAfterTenSec() {
  await tenSec()
  return 1
}
~~~
신로어싱크펑션 함수선언 await tenSec() 

$ async function{
  awit.tenSec()
  return 1
$ resolveAfterTensec().then.
}
// 어싱크펑션은 무조건 promise를 반환

## async
- 어싱크 문법쓰기위한 선언 함수 만들고 
- try 블록 안에서 리드파일 호출. promise반환
- await 키워드를 써서 promise를 기다리게함

<br>
---

# html5 hisroty api
예전 web은 문서수준, 지금 trello, slack보면 프로그램과 경계가 없어
자바스크립트로 페이지를 전환하고 url변경하는 방식 사용하기
(w3school 예전자료,  mdn가 웹표준 잘반영. 공부 기준삼기)    
- 브라우저 히스토리 조작하기   
<https://developer.mozilla.org/ko/docs/Web/API/History_API>

> 쌓아두는 구조의 자료형태 : stack 스택 

페이지 이동할때마다 history stack 쌓여
트렐로는 실제로 페이지 리로드를 하지않지만 사용자들이 뒤로가기 버튼 누르면 예상대로 
이동하기 위해서 스택에 직접 자바스크립트를 이용해서 쌓아서 튀어나오도록 로직을짠다.

~~~
$ history.back();
$ history.forward(); 
$ history.go() //1 ,-1 
$ history.length //스택에 쌓인개수 
~~~

> pushState()

> replaceState()

리엑트 라우터에서 우리대신 히스토리 api를 호출함
직접 쓸일은 없는데 디버깅을 위해서 알아두기  

- 웹서버를 쓸경우: 부드러운 화면전환효과 원할때  
- 싱글페이지 지만 pushState() 써서 about.html파일만들고 
- 웹서버는 www.home.com/index.html파일밖에 모르기때문에  
- www.home/#! : html문서를 다 부른뒤에 브라우저에서 해쉬백을 씀 
- www.home/#!/about  해쉬체인지나 이벤트핸들러등 




