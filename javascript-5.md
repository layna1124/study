
# Execution Context

## 1. 실행 컨텍스트
실행가능한 코드블럭이 실행되는 환경(코드블럭에 대한 정보들을 표현한것)
실행가능한 코드  
- Global Code : 진입함수없이 전역에쓴 코드는 그냥 실행됨 
- Function Code : 함수내에 쓴 코드들은 호출에 의해 실행 


## 2. 실행컨텍스트 객체의 프로퍼티

### 2-1. 변수객체 (VO/Variable Object)
- 변수, 매개변수와 인수(매개변수의 값), 함수선언 정보를 담는 객체이다

- 전역 컨텍스트가 가르키는 VO는 전역객체이며 매개변수와 인수가 없다. 
- 함수 컨텍스트는 함수객체 내부에 있는 매개변수와 인수들의 정보를 담은 아규먼트객체가 있다

- VO가 가리키는 객체 GO(전역객체)와 AO(활성객체)

### 2-2. Scope Chain (SC)
현재 실행 컨텍스트의 Activation Object를 선두로하여 순차적으로 상위 컨텍스트의 Activation Object를 가리키며 마지막 리스트는 전역 객체를 가리킨다.


## 3. 실행 컨텍스트의 생성 과정

~~~
var x = 'xxx';

function foo () {
  var y = 'yyy';

  function bar () {
    var z = 'zzz';
    console.log(x + y + z);
  }
  bar();
}
foo(); //함수를 호출하면 function foo () {}로이동 
~~~

### < 실행 컨텍스트 stack > 
: 스택은 선입후출 (먼저들어온 것이 가장 마지막에 나감) 
1. 실행하려고 들어온 순간 전역실행 컨텍스트를 만든다.
2. foo(); 전역에 있는 foo함수를 호출하면. foo함수의 실행컨텍스트가 만들어지고 전역위에 stack으로 쌓인다. 
3. bar () 함수의 실행컨텍스트가 만들어지고
4. 콘솔로그가 찍혀서 함수에서 탈출하면, bar()함수의 실행컨텍스트가 소멸된다.


(1) Scope Chain의 생성과 초기화
(2) 변수의 객체화 :
  -VO에 프로퍼티와 값을 추가 (변수와 함수 선언을 VO에 추가하여 객체화하기 때문) Global Code의 경우, VO는 Global Object이다.
  - 1. 함수코드는 

  (2-1) 함수 foo의 선언처리
  (2-2) 변수 x의 선언처리


(3) this value 결정
이 순차적으로 실행

<br><br>

<hr>
<br>

# 클로저 (closure)
-  일급 객체로 취급하는 함수형 언어
-  외부함수에 의해 내부함수가 반환된 이후에도 life-cycle이 유지되는 것

> 일반케이스 . 10이라고 잘찍힘
~~~
function outerFunc() {
  var x = 10;
  var innerFunc = function () { console.log(x); };
  innerFunc();
}

outerFunc();
~~~

> 클로저 
~~~
function outerFunc() {
  var x = 10;
  var innerFunc = function () { console.log(x); };
  return innerFunc;
}

var inner = outerFunc(); // 클로저의 형성
inner(); // 10
~~~ 

- 원래 innerFunc은 리턴되고 소멸되어야함. 근데 10이 나와
- AO에 실행컨텍스트가 사라졌음에도 변수 var= x가 살아있음
- 메모리는 사용되지 안으면 지워지는데 하나라고 참조하고 있으면 안지워짐.
- 외부함수 내에 있는 내부함수가 외부함수보다 오래 유지될때
변수가 살아있는 것처럼 유지되는것 
- 외부함수 outerFunc 함수실행 컨텍스트의 ao는 지워지지 안은것


## 클로저 활용

- 이벤트는 쭉가는게 아님
- add 증가
- 예제 많이 찾이보기 

### 1. 전역변수 사용억제 
~~~
  <!--클로저를 사용한 Counting-->
  <button type="button" onclick="myFunction()">Count!</button>
  <p id="demo">0</p>

  <script>
    var add = (function () {  //외부함수 
      var counter = 0;        //외부함수의 변수 =자유변수 
      return function () {    //내부함수 
        return counter += 1;
      }
    })();

    function myFunction(){
      document.getElementById('demo').innerHTML = add();
    }
  </script>
~~~

### 2. setTimeout()의 콜백함수
- 콜백함수도 더 오래 살아남을수 있다. 
~~~
<script>
    var fade = function (node) {
      // 자유변수
      var level = 1; // 
      var step = function() {
        var hex = level.toString(16); // 
        
        // hex: '1' ~ 'f'
        node.style.backgroundColor = '#ff' + hex; // 

        if(level < 15) { // 
          level += 1;
          setTimeout(step, 100); // 
        }
      };
      // setTimeout 호출 이후 fade 함수는 종료. 100ms 후 함수 step은 호출
      // 외부 함수 fade보다 내부 함수 step이 더 오래 유지
      setTimeout(step, 100); // ★
    };

    fade(document.body); // 
  </script>
~~~

fade라는 외부 함수 
step 이라는 내부함수 
level 을 참조하고 있다 

★ 100밀리 세컨드 단위로  계속 실행 15번 
외부함수의 자유변수는 살아있다. 

~~~
for (var i = 0; i < 5; i++){
  arr[i] = (function (id) { // ★
    return function () {
      return id; //
    };
  })(i); //  배열 arr에는 즉시실행함수에 의해 함수가 반환된다.
}
~~~
즉시실행함수는 i를 인자로 전달받고 
매개변수 id에 할당한 후 내부 함수를 반환하고 life-cycle이 종료된다. 
매개변수 id는 자유변수가 된다.

함수 레벨 스코프 특성으로 인해 for 루프의 초기문에서 사용된 변수의 스코프가 전역이 되기 때문에 발생하는 현상.  ES6의 let 키워드를 사용하면 해결된다. 


# 객체지향 프로그래밍

## 클래스기반언어 
클래스란?
같은 종류의 집단에 속하는 속성과 행위를 정의한것
new 연산자를 통한 인스턴스화 과정이 필요
자바에서는 class안에 class는 extend를 통해 간단해결



## 프로토타입 기반언어
클래스 개념이 없고 별도의 객체생성방법이 존재
- 객체리터럴,object()생성자함수,생성자함수
~~~
// 객체 리터럴
var obj1 = {};
obj1.name = 'Lee';

// Object() 생성자 함수
var obj2 = new Object();
obj2.name = 'Lee';

// 생성자 함수
function F() {}
var obj3 = new F();
obj3.name = 'Lee';
~~~

- 자바스크립트는 이미 생성된 인스턴스의 자료구조와 기능을 동적으로 변경할 수 있다
- 객체 지향의 상속, 캡슐화(정보 은닉) 등의 개념은 프로토타입 체인과 클로저 등으로 구현할 수 있다.


## 생성자 함수와 인스턴스의 생성 
- 객체생성 
- 생성된객체들의 상속관계
- 객체를 캡슐화 하는 방식 


생성자(Constructor)함수: 자바의 클래스개념, 그러나 함수라는것
~~~
// 생성자 함수
// 객체를 만들기위해 생성자함수 생성 
function Person(name) { 
  // 프로퍼티
  // this안쓰면 프로퍼티 추가할 방법 없어 
  this.name = name;   

  // 메소드1
  this.setName = function (name) {
    this.name = name;
  };

  // 메소드2
  this.getName = function () {
    return this.name;
  };
}

// me라는 인스턴스 생성
var me = new Person('Lee');
console.log(me.getName()); // Lee

// 메소드 호출
me.setName('Kim');
console.log(me.getName()); // Kim
~~~

메소드 여러개 쓰지않고  아래처럼 
person생성자 함수로 여러개의 인스턴스를 만들수있음  

~~~
var me  = new Person('Lee');
var you = new Person('Kim');
var him = new Person('Choi');
~~~
위는 각각의 인스턴스에 메소드 setName, getName이 중복생성.
인스턴스가 내용이 동일한 메소드를 각자 소유한다. 메모리 낭비 

따라서 프로토타입 체인과 메소드의 정의
~~~
function Person(name) {
  this.name = name;
}

// 프로토타입 객체에 메소드 정의
Person.prototype.setName = function (name) {
  this.name = name;
};

// 프로토타입 객체에 메소드 정의
Person.prototype.getName = function () {
  return this.name;
};

var me  = new Person('Lee');
var you = new Person('Kim');
var him = new Person('choi');

console.log(Person.prototype); 
// Person { setName: [Function], getName: [Function] }

console.log(me);  // Person { name: 'Lee' }
console.log(you); // Person { name: 'Kim' }
console.log(him); // Person { name: 'choi' }
~~~
Person 생성자 함수의 prototype 프로퍼티가 가리키는 프로토타입 객체로 이동시킨 setName. getName 메소드는 프로토타입 체인에 의해 모든 인스턴스가 참조가능. 
프로토타입 객체는 상속할 것들이 저장되는 장소이다.



## 자바스크립트의 상속 구현 방식

1. 의사클래스 패턴상속 : 과거사용 (new써야, 성자링크깨짐, 객체리터럴 못씀)

2. 프로토타입 패턴상속 : 
 Object.create 함수를 사용하여 객체에서 다른 객체로 직접 상속을 구현하는 방식
 순수한 자바스크립트 방식의 개발 
- 보통 프레임워크를 쓰기때문에 상속개념이 있을것. 위처럼 구현할 일은 거의없다.


## 캡슐화와 모듈 패턴

캡슐화 :은닉 

Java는 클래스 구성 멤버를 한정가능. 
public 메소드나 데이터는 외부에서 사용가능. 
private선언 외부에서 참조할 수 없음. 
js에서는 어떻게할까? 

클로저를 활용한 기본적은닉방법 
~~~
var person = function(arg) {
  var name = arg ? arg : '';

  return {
    getName: function() {
      return name;
    },
    setName: function(arg) {
      name = arg;
    }
  }
}
~~~
var person 객체리터럴임. 생성자함수아님 new없어
var = name 는 private 변수로 js는 내부함수 외부에서 참조 안되
(var 대신 this쓰면 public 으로 바뀜)
return{} 객체를 리턴함. 안에 함수 두개. 
getName, setName은 클로저로서 private 변수(자유 변수)에 접근





