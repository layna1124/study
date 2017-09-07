# Dom 문서객체모델 


## 1. DOM (Document object Model)
브라우저는 웹문서(HTML,XML,SVG)를 로드하고 파싱하여 DOM을 생성한다.

- 웹문서를 브라우저가 이해가능한 구조로 구성하여 메모리에 적재하는것이 DOM이다.
- 동적인 웹페이지를 위해 DOM에 접근하고 변경하는 프로퍼티와 메소드의 집합이 DOM API이다. 
- DOM은 각 객체에 접근하고 수정할수 있는 프로퍼티와 메소드를 제공하며 DOM이 수정되면 브라우저를 통해 사용자가 보게될 내용이 변경된다. 

- 브라우저에 따라 DOM종류가 다르다.

- SPA는 DOM조작으로 모든 페이지를 생산한다. HTML을 하나로 만들어서 한번만 로딩하고 그뒤로는 AJAX만 불러온다. 빠르고 어플리케이션 사용하는 느낌이다. (REACT VUE 등)

<br>

## 2. DOM tree
브라우저가 HTML문서를 로드한후 해당 문서에 대한 모델을 메모리에 생성한다.

- DOM에서의 모든 요소, 어트리뷰트, 텍스트는 하나의 객체로 Document객체의 자식이다. 

- tree구조에서는 객체를 노드라고 한다.

- DOM tree의 구성  
(1) 문서노드 (document Node) : tree의 최상단, 시작점  
(2) 요소노트 (Element Node) : html상의 요소와 대응되며 부자관계를 형성  
(3) 어트리뷰트 노드 (Attribute Node) : 요소노드와 형제관계   
(4) 텍스트노드 : 요소노드의 자식으로 dom tree의 최종단   

![돔트리객체구조](http://poiemaweb.com/img/HTMLElement.png)

- 크롬 개발자도구에서 properties확인이 가능하다.

- Dom을 통해 웹페이지를 조작을 하려면 ?
: 조작하고자 하는 요소를 탐색하고 


- DOM api가 브라우저 버전을 많이 타기 때문에 방어코드가 필요한 불편함이 있어서, 제이쿼리가 등장함. 간편하고 직관적이나 개발방법론의 변화로 (요소명,어트리뷰트명을 써야해 = 자바스크립트가 HTML코드에 의존한다. 이것이 분리되어야지 불합리하다는 의견에 의해 react, angular가 나와)


## DOM Query (요소에의 접근)

### 1. 하나의 요소노드 선택 

> document.getElementById(id)  

- id값을 문자열''로 준다.
- 모든 브라우저 동작 

> document.querySelector(cssSelector)

- 복수개가 선택된 경우, 첫번째 요소만 반환
- IE8 이상의 브라우저에서 동작 (IE8도 불완전)



### 2. 여러개 요소노드 선택 
> document.getElementsByClassName(class)

- class 어트리뷰트 값으로 요소 노드를 모두 선택
- IE9 이상 

~~~
// HTMLCollection을 반환한다.
var elems = document.getElementsByClassName('red'), i;

for (i = 0; i < elems.length; i++) {
  // 클래스 어트리뷰트의 값을 변경한다.
  elems[i].className = 'blue';
}
~~~

- 여러개 요소 노드들을 반환하기 위한 객체로 유사배열 형태로 반환 
- HTMLCollection는 실시간으로 Node의 상태변경을 반영한다.
- 문제 :   
red클래스명이 blue로 바뀌는 순간. live로 html컬렉션에서 빠짐. 그래서 length가 줄어들고 예상되로 실행되지 안음

> 해결법 :     
(1) for문을 역방향으로   
(2) while문을 무한 반복   
(3) 유사배열을 배열로 변환   
(4) querySelectorAll 메소드 사용 (non-live) 

프레임워크를 쓰게되면 (4)와같이 쓸일이 없고 그안에 맞는 규칙을 따라야한다. 어플리케이션을 만들면 위처럼 쓰게될것이고, 홈페이지 수준이면 jquery를 쓰면 간단하다. 제이쿼리 1.대는 ie하위버전까지 대응하지만 무겁다. 

> document.getElementsByTagName(tagName)
- 태그명을 쓰면 live로 변경되도 크게 문제가 없다. 
- 모든 브라우저 동작 

> document.querySelectorAll(selector)

- 지정된 CSS 선택자를 사용하여 요소 노드를 모두 선택 ('li.red')
- IE8이상 동작 


## DOM Traversing (탐색)

> ParentNode

- 부모노드를 탐색
- 모든 브라우저 동작 

~~~
var elem = document.getElementById('two');
var parentNode = elem.parentNode;
parentNode.className = 'blue';
// 두번실행 해야할경우 변수에 담아서 한번만 실행
~~~

> firstChild, lastChild

- 자식노드를 탐색
- IE9 이상
- 공백을 텍스트로 인식하므로 오류 
- 공백 제거하거나 jQuery: .prev() .next() 사용  
~~~
var elem = documentㄴㄴ.getElementsByTagName('ul')[0];//
elem.firstChild.className = 'blue';  
elem.lastChild.className = 'blue';
// 작동하지 안음 

<ul>       // 공백
 <li></li> // 2번째로인식함  
 <li></li>
</ul>
~~~

> hasChildNodes()  
- Boolean값 반환 
- 모든브라우저 

> childNodes 
- 자식노드 컬렉션반환
- 모든 브라우저

> previousSibling, nextSibling 
- 형제노드 탐색
- IE9 이상 
~~~
var elem = document.getElementsByTagName('ul')[0];

// first Child
elem.firstChild.className = 'blue';
// 2nd Child
elem.firstChild.nextSibling.className = 'blue';
// 3rd Child
elem.lastChild.previousSibling.className = 'blue';
// last Child
elem.lastChild.className = 'blue';
~~~

## DOM 조작

### (1) 텍스트 노드의 접근/수정 
~~~
// 해당텍스트 노드의 부모요소 노드 선택
var one = document.getElementById('one');
console.dir(one); // HTMLLIElement: li#one.red

// firstChild 프로퍼티를 사용 텍스트 노드를 탐색
var textNode = one.firstChild;

// nodeValue 프로퍼티를 사용 노드의 값을 취득
console.log(textNode.nodeValue); // Seoul

// nodeValue 프로퍼티를 이용 텍스트를 수정
textNode.nodeValue = 'Pusan';
~~~


### (2) 어트리뷰트 노드에의 접근/수정

> hasAttribute(attribute)
속성 있는가 검사 

> getAttribute(attribute)
값을 반환  

> setAttribute(attribute, value)
값을 줌 

> removeAttribute(attribute)
속성제거 

~~~
var four = document.getElementById('four');

// four에 class 어트리뷰트가 존재하지 않으면
if (!four.hasAttribute('class')) {
  // four에 name 어트리뷰트를 추가하고 값으로 'user'를 설정
  four.setAttribute('class', 'blue');
} else { // four에 class 어트리뷰트가 존재하면
  four.className = 'blue';
}

// four에 lang 어트리뷰트의 값을 취득
console.log(four.getAttribute('class')); // blue

// four에서 name 어트리뷰트를 제거
four.removeAttribute('class');

// inputUser에서 name 어트리뷰트의 존재를 확인
console.log(four.hasAttribute('class')); // false
~~~


### (3) HTML 콘텐츠조작

> textContent
- 순수 텍스트만 지정 

> innerText
- 비표준

> innerHTML
- 모든 콘텐츠를 하나의 문자열로 취득. 마크업포함 
- 마크업이 포함된 콘텐츠 추가는 보안에 취약
(스크립트 태그를 넣지않는 등의 대응필요)


### (4) DOM 조작방식

innerHTML 프로퍼티를 사용하지않고 DOM을 직접 조작하여 콘텐츠를 추가할수있다.
정교하게 위치지정이 가능하다. 

> createElement(tagName)
- 요소생성
> createTextNode(text)
- 텍스트를 인자로 전달하여 텍스트노드생성
> appendChild(Node)
- 인자로 전달한 노드를 자식요소로 dom트리에 추가
> removeChild(Node)
- 인자로 전달한 노드를 dom트리에서 제거 

~~~
// 요소생성.아직추가안됨
var newElem = document.createElement('li'); 

// 텍스트노드생성
var newText = document.createTextNode('Beijing');

// 텍스트 노드를 newElem자식으로 append써야 추가 
newElem.appendChild(newText); 
~~~
 
※ innerHTML과 insertAdjacentHTML()은 크로스 스크립팅 공격(XSS: Cross-Site Scripting Attacks)에 취약하다. 텍스트를 추가 또는 변경시에는 textContent, 새로운 요소의 추가 또는 삭제시에는 DOM 조작 방식을 사용하도록 한다.
대응방안 <http://skynarciss.tistory.com/41>



### style  
style 프로퍼티를 사용하면 inline 스타일 선언을 생성한다.
~~~
var four = document.getElementById('four');
four.style.color = 'blue';
four.style.fontSize = '2em';
~~~

===

## Ajax
자바스크립트를 이용해서 비동기적으로 서버와 브라우저가 데이터를 교환할수 있는 통신방식 이다.

새로운 html울 로드하는 과정에서 화면이 깜빡거리는 현상이 있는데
페이지의 일부만 갱식하여 빠른 퍼포먼스와 부드러운 화면표시 효과를 기대할수 있다.

서버는 HTML, XML, JSON을 반환하는데
Ajax을 위한 데이터형식은 JSON을 사용하는것이 일반적이다. 

## 동기식처리 vs 비동기식 처리 

### 동기식 (blocking)
ex) alert 요청받을때까지 시스템 모두 중단

### 비동기식 (non-blocking)
DOM 이벤트와 Timer함수, Ajax 요청시 순차적으로 동작하지 않는다


## 이벤트 루프와 동시성
![](http://poiemaweb.com/img/event-loop.gif)

브라우저는 단일 쓰레드(single-thread)에서 이벤트 드리븐(event-driven) 방식으로 동작한다.


서버에는ajax방식으로 요청을하지만
전체는 비동기식으로 돌고 그안에 이벤트가 있어

자바스크립트는 비동기를 못해, 
비동기 처리는 브라우저가 한다.


## Ajax요청 및 응답처리
브라우저는 XMLHttpRequest 객체를 이용하여 Ajax 요청한다.
~~~
// XMLHttpRequest 객체의 생성
var req = new XMLHttpRequest();

// 비동기 방식으로 Request를 오픈
req.open('GET', 'data/test.json', true);

// Request를 전송
req.send();
~~~

받는 처리는 이벤트로 
XMLHttpRequest.readyState 프로퍼티가 변경(이벤트발생)되면 이 함수(콜백함수.이벤트핸들러)를 호출 
~~~ 

req.onreadystatechange = function (e) {
  // 상태를 반환
  // 4 = DONE 서버응답완료 = 데이터가왔다 
  if (req.readyState === XMLHttpRequest.DONE) {
    // status는 response 상태코드를 반환 : 200번 정상응답
    if(req.status == 200) {
      //req는 우리가 만든객체
      //responseText라는 프라퍼티가있어
      //요청한 데이터는 이안에 들어있어 
      console.log(req.responseText);
    } else {
      console.log("Error!");
    }
  }
};
~~~

> XMLHttpRequest.open() : 서버에 요청준비 

> XMLHttpRequest.send() : 서버에 전달

> XMLHttpRequest.onreadystatechange  
: Response가 클라이언트에 도달하여 발생된 이벤트를 감지하고 콜백함수를 실행, 이벤트핸들러 

> XMLHttpRequest.responseText   
: 서버응답 정상일때 서버에서 전송한 데이터가 담기는곳

<br>

## Load JSONP
요청에의해 전달된 웹페이지가 서버와 동일한 도메인이 아닐때 보안상의 이유로 데이터처리가 제한된다.

### 동일출처원칙 우회방법 
(1) 웹서버의 프록시(Proxy) 파일  
: 서버에 원격서버로부터 데이터를 수집하는 별도기능 추가

(2) **JSONP**  
: script 태그에는 주소제약이 없음으로, 자신의 서버에 함수를 정의하고 다른 서버의 데이터를 인수로 하는 함수 호출문을 로드한다.


---

## 이벤트의 종류 

> UI Event
- load(로드완료시), unload(새페이지요청한경우), error, resize, scroll, select(텍스트선택)

> Keyboard Event
- keydown, keyup, keypress(키누르고뗏을때)

> Mouse Event
- click, dbclick, mousedown, mouseup(누르고있던 마우스버튼뗄때, 
- (터치스크린에서 동작안함)mousemove, mouseover, mouseout

> Focus Event
- focus/focusin,  blur/focusout 

> Form Event
- submit(폼태그내용전부보낼때, ajax는 form태그 안써)

> Clipboard Event
- cut, copy(콘텐츠복사, 막을수도),paste

## 이벤트 Binding 
### HTML Event Handler
html요소에 이벤트를 대응시킨다
~~~
  <button onclick="myFunction()">Click me</button>
  <script>
    function myFunction() {
      alert('Button clicked!');
    }
  </script>
~~~
오래된 코드들에서 사용된다. html와 js는 분리되어야한다.

### DOM EventHanler 방식
이벤트 핸들러에는 하나의 함수만이 바인딩 되기때문에 인수를 전달할수 없는 단점이 있다. addEventListener 방식을 사용하여 해결한다

### addEventListener
- 해당 이벤트가 발생했을 때 실행될 콜백 함수를 지정한다.
- 하나의 이벤트에 대해 하나 이상의 핸들러를 추가할 수 있다.
- IE8이하는 attachEvenr()함수를 사용

~~~
// 방어코드 
if (elem.addEventListener) {    // IE 9 ~
  elem.addEventListener('click', func); 
} else if (elem.attachEvent) {  // ~ IE 8
  elem.attachEvent('onclick', func);
}
~~~

진입점 .documents  (dom내에 있는 요소에 대해서 실행하겠다)
타깃 안쓰면 window (전부먹힘: 스크롤 등)
~~~
<script>
    addEventListener('click', function() {
      alert('Clicked!');
    });
</script>
~~~

input요소를 blur이벤트에 바인딩 
인풋에 값이 안써졌을때 blur이벤트(마우스가 빠졌을때 체크)  
2자 이상이라는 규칙을 상수화, 함수의 인수로 전달
~~~
function foo() {
  alert('clicked!');
}
// elem.addEventListener('click', foo()); //대기하지 않고 바로 실행되므로 쓸수없다. 
elem.addEventListener('click', foo);      // 이벤트 발생 시까지 대기
~~~

~~~
  <label for="username">User name </label>
  <input type="text" id="username">
  <em id="message"></em>
  <script>
      var MIN_USER_NAME_LENGTH = 2; // 이름 최소 길이

      var elem = document.getElementById('username');
      var msg  = document.getElementById('message');

      function checkUserNameLength(n) {
        if(elem.value.length < n) {
          msg.innerHTML = '이름은 ' + n + '자 이상이어야 합니다';
        } else {
          msg.innerHTML = '';
        }
      }

      elem.addEventListener('blur', function() { //여기 function()에 위의함수불러
        checkUserNameLength(MIN_USER_NAME_LENGTH);
      });

  </script>
~~~


6. 핸들러함수 내부의 this
6.1 HTML Event Handler
: this는 window
6.2 전통적(Traditional) DOM Event Handler
: this는 이벤트에 바인딩된 요소
6.3 DOM Level 2 Event Listener
: 이벤트 핸들러가 바인딩 되어있는것. 

## 이벤트의 흐름
- 버블링 : 자식요소에섭 발생한 이벤트가 부모요소로 전파 
- 캡처링 : 반대. ie8이하 지원불가 . 캡처링은 버블링으로 끝남
- true: capturing / false: bubbling

- 버블링 캡쳐링을 선언하지 안으면 html부터 내려와서 버블링되어 종료되는데
어느하나에만 반응하게 설정한경우 , 
- 캡처링만 설정시 : 다시 버블링되어 올라갈때엔 반응하지 않는다.
- 버블링만 설정시 : 캡처링되어 내려올땐 반응하지 않는다.
- 어떨때 이렇게 쓰는가?

## 이벤트객체

~~~
  <p>클릭하세요. 클릭한 곳의 좌표가 표시됩니다.</p>
  <em id="message"></em>
  <script>
  function showCoords(e) { // e: event object
    var msg = document.getElementById('message');
    msg.innerHTML =
      'clientX value: ' + e.clientX + '<br>' +
      'clientY value: ' + e.clientY;
  }
  addEventListener('click', showCoords);
  </script>
~~~
(e)이벤트 오브젝트를 담을 객체다. event라고도 쓰는데 보통 e라고 씀.
뭐라고 써도 상관없어. 첫번째 매개변수로 명시적으로 선언. 안쓰면?
이벤트가 발생한시점에 브라우저가 암묵전으로 셋팅함. event 객체는 암묵적으로 전달. 
두번째 인자부터는 개발자가 매개변수 정의하면됨 

(e)이벤트객체를 갖음. 타겟은 이벤트를 발생한요소

## 이벤트 프로퍼티

### Event.target
이벤트를 발생시킨 요소를 가리킴.
~~~
 <button>Hide me</button>
  <script>
  function hide(e) {
    e.target.style.visibility = 'hidden';
  }
  document.querySelector('button').addEventListener('click', hide);
  </script>
~~~

### Event.currentTarget
이벤트 리스너에 바인딩된 요소, this

> e.keyCode : 키보드이벤트가 발생했을때 

> Event.cancelable : 기본동작취소여부(true/false)
~~~
  var elem = document.querySelector('a');
  elem.addEventListener('click', function (e) {
    console.log(e.cancelable);
    e.preventDefault(); //링크이동안함 
  });
~~~

> Event.eventPhase : 이벤트 흐름상에서 어느 단계 인지

0 : 이벤트없음/ 1: 캡처링단계/2:타깃/3:버블링단계


### Event Method

> Event.preventDefault()

> Event.stopPropagation()

## 이벤트 위임
다수의 자식 요소에 이벤트 핸들러를 바인딩하는 대신에  
하나의 부모 요소에 이벤트 핸들러를 바인딩하는 방법

사용예제)
~~~
<ul id="parent-list">
  <li id="post-1">Item 1</li>
  <li id="post-2">Item 2</li>
  <li id="post-3">Item 3</li>
  <li id="post-4">Item 4</li>
  <li id="post-5">Item 5</li>
  <li id="post-6">Item 6</li>
</ul>
~~~

DOM 트리에 새로운 li 요소를 추가하더라도 이벤트 처리는 부모 요소인 ul 요소에 위임되었기 때문에 새로운 요소에 이벤트를 핸들러를 다시 바인딩할 필요가 없다.
이벤트 흐름에 의해 이벤트를 발생시킨 요소의 부모 요소에도 영향(버블링)을 미치기 때문에 가능
이벤트를 발생시킨 요소를 알아내기 위해서는 Event.target을 사용

- li에 클릭이벤트 핸들러를 바인딩하면 6개 이벤트 핸들러를 바인딩함 
- 
- 몇번째 li가 클린되었는지 알고싶을때 : 이벤트 타깃을 쓴다  

~~~
<script>
    var msg = document.getElementById('msg');

    document.getElementById('parent-list').addEventListener('click', function (e) {
      console.log('[target]: ' + e.target);
      console.log('[target.nodeName]: ' + e.target.nodeName);

      // e.target가 true이면 =='li' 이 구문을 실행
      // 클릭된 이벤트 요소가 li인가 (true) 

      if (e.target && e.target.nodeName == 'LI') {
        msg.innerHTML = 'li#' + e.target.id + ' was clicked!';
      }
    });
</script>
~~~


## 기본 동작의 변경
이벤트 객체는 요소의 기본 동작과 요소의 부모 요소들이 이벤트에 대응하는 방법을 변경하기 위한 메소드는 가지고 있다.

> Event.preventDefault()

> Event.stopPropagation()

: 이벤트의 전파(propagation: 버블링, 캡처링)를 중단

> preventDefault & stopPropagation

: 버블링 또는 캡처링의 중단을 동시에 실시
: return false 는 바닐라에서 안먹히고 제이쿼리에서만씀 
~~~
//$ 쿼리셀렉트올 같은것 
$('a').click(function (e) {
    e.preventDefault(); // OK 제이쿼리안에 바닐라씀 
  });
~~~


