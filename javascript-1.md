> Coding

코딩(프로그래밍)이란, 컴퓨터가 이해할 수 있는 언어, 즉 코드를 사용해 컴퓨터에 명령과 정보를 만드는 작업


> 컴파일러(compiler)

사람이 이해하는 문법(Syntax)을 사용하여 프로그램을 작성한 후,컴퓨터가 이해할 수 있는 기계어로 변환


> Syntax (문법)

사람이 이해하는 언어 

> Semantics (의미)

의미부여를 위해 프로그래밍 언어는 변수와 값, 키워드, 연산자, 표현식, 조건문과 반복문에 의한 흐름제어(Flow control), 구문(Statement), 구문의 집합인 함수 그리고 객체, 배열 등의 자료구조를 제공


## Javascript
---

* HTML, CSS와 함께 웹을 구성하는 요소중 하나로 웹브라우저에서 동작하는 유일한 언어

* C, Java에서 많은 문법을 차용

* 플랫폼을 위한 모바일 웹/앱 개발 분야에서도 주목. 웹은 물론 모바일 하이브리드 앱(PhoneGap, Sencha Touch, Ionic), 서버 사이드(NodeJS), Desktop(Electron, AppJS), 로봇 제어(Cylon.js, NodeBots) 언어로서 가장 인기있는 언어

* SPA(Single Page Application) 웹 앱이 대중화되면서 Angular, React, Vue.js 등 다양한 SPA Framework/Library 사용

* jQuery의 등장으로 DOM(Document Object Model)를 보다 쉽게 제어

* 자바스크립트는 인터프리터 기반의 언어로써 실행과 동시에 소스 코드가 화면에 반영. 


> 인터프리터 언어 (interpreter language)

목적 파일 산출 과정이 없이 실행과 동시에 줄 단위로 번역. 저용량 소스에 적합. HTML파일 안에 직접 기술가능. 
소스 코드의 길이가 긴 경우에는 실행 속도가 느림. 사전 컴파일이 없어서 에러찾기 힘들수있음.

※ NodeJS는 V8 자바스크립트 엔진 기반으로 돌아가는 프레임워크. 기존 컴파일러의 장점과 인터프리터의 장점을 섞은 형태


* 자바스크립트는 프로토타입 기반의 객체지향 언어 (클래스가 없어서 함수지향언어라고 듣기도함)

* Node.js 등장으로 광범위하게 사용되는 Full stack 개발 언어가됨. 웹 브라우저에서만 동작하는 반쪽짜리 언어 취급에서 Front-end 영역은 물론 Back-end 영역까지 아우르는 웹 프로그래밍 언어가됨. 그러나 계속 변화하는 중이라 공부해야함. 자바는 고착되서 잘하는 사람이 많고 시장넓은데 SI업체들.


링크  
https://stackoverflow.com (스택 오버플로우) 
검색 1위 자바스크립트 2위 sql : 백엔드에서 중요 3위 java 



브라우저 동작원리
----
렌더링엔진(html, css)과 자바스크립트엔진 

브라우저는 서버로부터 html, css, javascript 파일을 응답받음. html, css 파일은 렌더링 엔진의 HTML 파서와 CSS 파서에 의해 파싱(Parsing)되어 DOM, CSSOM 트리로 변환되고 렌더 트리로 결합됨.

HTML 파서는 script 태그를 만나면 DOM 생성 프로세스를 중지하고 자바스크립트 엔진에 제어 권한을 넘김. 자바스크립트 엔진의 실행이 완료된 후 브라우저가 중지했던 시점부터 DOM 생성을 재개함. 따라서 script 태그의 위치에 의해 DOM의 생성이 지연될 수 있음. body직전에 스크립트 넣는것은 dom이 생성된뒤에 document.를 건드리려고 하는것. css는 head에 넣어서먼저 파싱되는것엔 이의가없음

![Alt ](http://poiemaweb.com/img/client-server.png
)


대부분의 프로그래밍 언어는 운영체제 위에서 실행되지만 웹 애플리케이션의 JavaScript는 브라우저의 틀 안에서 HTML, CSS와 함께 실행.


> DOM
동일한 문서를 표현하고, 저장하고, 조작하는 방법을 제공. DOM 은 웹 페이지의 객체 지향 표현이며, 자바스크립트와 같은 스크립팅 언어를 이용해 수정할 수 있다.


ECMA Script
----

에크마 스크립트 4버전이 무산되어 6버전에 대폭 추가되는바람에 5만큼의 양이 6버전에 추가됨. 지금 8버전이 나옴(2017) 매년 업그레이드 예정이지만 양은 줄어들것.
6버전만 배워도 충분 우리가 할것.브라우저 서포트안됨. 5버전도 (ie9이상만 작동).  babel 바벨사용하면 7문법도 사용가능.


<배울내용>
- typescript 는 angular 에서 사용
- webpack


> Hello World
~~~

  <h1 id="demo">My Web Page</h1>
  <button type="button" onclick="myFunction()">Click me</button>
  <script>
    function myFunction() {
      var myHeader = document.getElementById('demo');
      myHeader.innerHTML = 'Hello world!';
    }
  </script>

~~~

getElementById : 아이디로 요소를 가지고 오라.  
innerHTML : 안에 요소를 바꿔라 

> 외부실행

script 요소를 만나면 웹페이지의 파싱을 잠시 중단. 그래서 로딩지연되는걸 막기위해 async와 defer (웹페이지 파싱과 외부 스크립트 파일의 다운로드가 동시에 진행)쓰지만 ie9이상만 작동.

~~~
<script async src="extern.js"></script>
<script defer src="extern.js"></script>
~~~

![Alt ](http://poiemaweb.com/img/script-execution.jpg)



Javascript Syntax Basics
---

> 구문 (Statement)
: 각각의 명령

 실행되면 무슨 일인가가 일어나게 된다
 구문은 값(Value), 연산자(Operator), 표현식(Expression), 키워드(Keyword), 주석(Comment)으로 구성되며 세미콜론( ; )으로 끝나야 한다.

- 코드블럭 :중괄로까지 ({…})



> 표현식
: 값 하나로 수용

자바스크립트는 문자열(문자여러개)과 문자열을 더할수(붙일수..이을수 +연산자있으면 )있다


> Variable 변수  

: 인간이 알수있는 이름 = 식별자   
: 값을 일시적 저장해야 할때   
: 컴퓨터는 기억하려면 메모리가 필요. 메모리와 관게가있어.  
저장하면 찾아와야지. 메모리 길쭉한 바모양으로 한칸씩 (1byte) 나눠져있고 각각의 주소가있어. 이 칸의 개수따라
메모리 용량 2g가냐 4g가냐. 클수록 많은 어플리케이션 돌려도 문제가없다. 기억할게 많으니까 메모리가 커야되.
메모리적으면 안쓰는거 지워서 간신히 쓰고..못버티면 죽는거야.  
메모리의 일련번호가 쫙~ 메겨져 있어.주소가 모두 있는데 복잡. 인간모르고 자바스크립트는 알지.
인간이 보기쉽게 이걸 변수 이름을 지어.

> 저장하다=할당  

> 선언과 초기화가 다른것?
- 선언은 메모리 영역을 확보하고 언디파인드값을 집어넣음. (값이있음)
  생성된 이후 최초로 값을 넣는것을 초기화 라고함 
- 그래서 언디파인드라는 가짜값을 갖고있다가 초기화하는 진짜값이 처음 들어감



> 네이밍 

통상 아래처럼 쓴다. 
: html, css 값에 "" 쌍따옴표   
  자바스크립트는 '' 홀따옴표    






## 기타  

- 노드환경 : server-side. vscode에서 출력되는거 노드의 환경 돔컨트롤 안되지만 네트워크 기능이 추가. 여러파일 하나씩 읽기   
- 자바스크립트 엔진 : client-side. 돔을 컨트롤 할수있음. 크롬브라우저 개발자도구 콘솔, 윈도우에선 프롬프트라고 깜빡거림 
- 위 둘이 중복되는 부분이 많아서 자바스크립트 엔지니어가 서버사이드로 이동하기 쉬워짐 


#### REPL
> "repl에서 돌려봐" : 터미널에서 노드환경 들어가서 코딩하는것   
~~~
$ node
~~~
- 기초문법은 같기때문에 vscode에 출력하면서 보는데 문제없음      

===  
 

> 자바스크립트는 1급객체를 지원한다. 

변수(variable)에 담을 수 있다
인자(parameter)로 전달할 수 있다
반환값(return value)으로 전달할 수 있다
