
# 프로토타입과 객체지향  

- 자바는 클래스기반이고 객체지향언어이다. 
- 자바스크립트는 프로토타입 기반의 객체지향언어 이다. 부모객체가 있다.



### 자바스크립트의 객체 생성 방법
- 자바스크립트의 모든 객체는 자신의 부모역할객체와 연결되서 부모객체의 프로퍼티 또는 메소드를 상속받아 사용.
- 이러한 부모 객체를 Prototype(프로토타입)객체 라고한다. 

> 프로토타입객체 = 프로토타입 = 부모객체

> 브라우저에 __proto__ 라고 표시된다 = [[prototype]]이다. 


__proto__ : 부모찾는 기능뿐
[[prototype]] : 부모역활의 위치를 가리키는 링크다


![alt=""](http://poiemaweb.com/img/printout_student_obj_from_chrome.png)



## constructor 프로퍼티

- 프로토타입 객체는 constructor프로퍼티를 갖는다. 
- 자신을 생성한 객체를 가리킨다.
~~~
function Person(name) {
  this.name = name;
}
var foo = new Person('Lee');

// Person() 생성자 함수에 의해 생성된 객체를 생성한 객체는 Person() 생성자 함수이다.
console.log(Person.prototype.constructor === Person);

// foo 객체를 생성한 객체는 Person() 생성자 함수이다.
console.log(foo.constructor === Person);

// Person() 생성자 함수를 생성한 객체는 Function() 생성자 함수
// 
console.log(Person.constructor === Function);
~~~
- student.constructor 를 치면 student객체에서 컨스트럭터 프로퍼티를 찾는데 없으니까, 위로 올라가 이것을 Prototype chain 라고함. 


## Prototype chain (프로토타입체인)
- 자바스크립트는 특정 객체의 프로퍼티나 메소드에 접근하려고 할 때 
  해당 객체에 접근하려는 프로퍼티 또는 메소드가 없다면 
  [[Prototype]] 프로퍼티가 가리키는 링크를 따라 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티나 메소드를 차례대로 검색한다. 

~~~
// 선언과 동시에 생성. 개발자편의
var student = {
  name: 'Lee',
  score: 90
};

// student에는 hasOwnProperty 메소드가 없지만 아래 구문은 동작
console.log(student.hasOwnProperty('name')); // true

 console.log(student.__proto__ === Object.prototype); // true
console.log(Object.prototype.hasOwnProperty('hasOwnProperty')); // true
~~~
- 왜?: student 객체의 [[Prototype]] 프로퍼티가 가리키는 링크를 따라가서 student 객체의 부모역할을 하는 프로토타입 객체(Object.prototype)의 메소드 hasOwnProperty를 호출하였기 때문





> 함수(funtion)는객체=객체는=참조값을 갖는다  
- 호출할 수 있다.
- 일반 객체와 차이가 있다. 함수객체는 일반 객체에없는 프로토타입과 프로퍼티가 있다.
- 프로토타입과 프로퍼티는 자신이 생성할 객체의 부모역활할 객체를 가르킨다 (옆에서 가리키고 위에서 가리키고 의 차이)


## 우리가 객체생성 하는방식  (1)리터럴 (2)생성자함수  

### 1. 객체 리터럴 방식으로 생성된 객체의 프로토타입 체인
- 객체 리터럴을 사용하여 객체를 생성한 경우, 그 객체의 프로토타입 객체는 Object.prototype이다.


### 2. 생성자 함수로 생성된 객체의 프로토타입 체인
- 생성자 함수로 객체를 생성하기 위해서는 우선 생성자 함수를 정의하여야 한다.

- 함수를 정의하는 방식
 + 함수선언식(Function declaration)
 + 함수표현식(Function expression)
 + Function() 생성자 함수

- 3가지 함수 정의 방식은 결국 Function() 생성자 함수를 통해 함수 객체를 생성한다, 따라서 어떠한 방식으로 함수 객체를 생성하여도 모든 함수 객체의 prototype 객체는 Function.prototype이다. 생성자 함수도 함수 객체이므로 생성자 함수의 prototype 객체는 Function.prototype이다.

~~~
function Person(name, gender) {
  this.name = name;
  this.gender = gender;
  this.sayHello = function(){
    console.log('Hi! my name is ' + this.name);
  };
}

var foo = new Person('Lee', 'male');

console.dir(Person);
console.dir(foo);

console.log(foo.__proto__ === Person.prototype);                // ① true
console.log(Person.prototype.__proto__ === Object.prototype);   // ② true
console.log(Person.prototype.constructor === Person);           // ③ true
console.log(Person.__proto__ === Function.prototype);           // ④ true
console.log(Function.prototype.__proto__ === Object.prototype); // ⑤ true
~~~
![alt=""](http://poiemaweb.com/img/constructor_function_prototype_chaining.png)

~~~
//Function이 Person생성자 함수의 constructor
console.log(Person.__proto__ === Function.prototype);
~~~ 

## 기본자료형(Primitive data type)의 확장

- 값이 되는것은 다 리터럴 
- 기본자료형(숫자, 문자열, boolean, null, undefined)을 제외한 모든것은 객체인데 기본자료형인 문자열이 흡사 객체처럼 동작한다.
- 기본 자료형은 상속개념이 없어. 그냥 그 값자체. 문자열에 프로퍼티도 없고 메서드도 없잖아

~~~
// [1] 
var str = 'test';
console.log(typeof str);                 // string
console.log(str.constructor === String); // true
console.dir(str);

// [2]
var strObj = new String('test');
console.log(typeof strObj);                 // object
console.log(strObj.constructor === String); // true
console.dir(strObj);

console.log(str.toUpperCase());    // TEST
console.log(strObj.toUpperCase()); // TEST
~~~
- [1]처럼 써도 되고 [2]처럼 써도되 
- 이 string문자열을 값으로 갖고있는 객체는 ..이란 뜻 
  var strObj = new String('test');
-  편의기능 사용위해 객체화 해야되 
- 리터럴로 만들어도 .을 붙인순간 객체화 되고 
그 구문이 끝나면 다시 기본자료형으로 돌려주는 친절한js 

※ 기본자료형으로 프로퍼티나 메소드를 호출할 때 기본자료형과 연관된 객체로 일시적으로 변환되어 프로토타입 객체를 공유하게 된다.

- String 객체의 프로토타입 객체 String.prototype에 메소드를 추가하면 기본자료형, 객체 모두 메소드를 사용할 수 있다.
~~~
var str = 'test';
String.prototype.myMethod = function () {
  return 'myMethod';
};
console.log(str.myMethod());      // myMethod
console.log('string'.myMethod()); // myMethod
console.dir(String.prototype);
~~~

- 문자열에 . 붙여서 모든걸 쓸수있게 하면 느려질수 있음. 미리만들어두기?

## 프로토타입 객체의 변경
- foo의 부모객체를 바꿀수있어? 왜?
- 객체가 생성된 이후에도 상속관계를 변형시키고 싶을때 (자바에선 택도없는이야기)
- 
~~~
person.prototype={}; //빈객체로 넣으면..부모객체 바껴
~~~

~~~
function Person(name) { //생성자함수 
  this.name = name;
}
var foo = new Person('Lee');

Person.prototype = { gender: 'male' }; // 프로토타입 객체의 변경
var bar = new Person('Kim');//똑같은 생성자 함수에 new
~~~

- 자바스크립트는 es6에서 더욱 자바처럼됨. 자바하는사람많아서 
- 타입스크립트를 쓰면 거의 자바와 비슷 


## 프로토타입 체인 동작 조건

- 객체의 프로퍼티를 참조하는 경우, 해당 객체에 프로퍼티가 없는 경우, 프로토타입 체인이 동작한다.

<hr>

# Scope

- 스코프(유효범위)변수가 가지고 있는 참조 범위
  (유효하다=참조=접근 )
- 스코프는 변수가 갖는것

> (1) 전역scope = global scope 
  :변수가 전역에 선언, 코드 어디서든지 참조

> (2) 지역scope = local scope, funcion-level scope
  : 변수가 지역에서 선언,

- 함수 코드블럭(함수 내부에 선언된 변수) 만이 지역스코프 이다. 
  그 이외는 모두 전역스코프 이다.
~~~
var x = 0;
{
  var x = 1;
  console.log(x); // 1 ,js에선 중복선언
}
console.log(x);   // 1
~~~ 

~~~
let y = 0;
{
  let y = 1;
  console.log(y); // 1
}
console.log(y);   // 0
~~~ 
- ES6에서 도입된 let keyword 사용시 block-level scope를 사용

## 

## Global scope

- 바깥에 나와있어. 그냥 전역변수=전역함수 
~~~
 // 전역에서 변수선언
 // 전역 객체(Global Object) window의 프로퍼티 
var global = 'global';
~~~

- 외부에서 참조 불가능한 변수. 프라이빗 
- 생성자함수 경우 this 퍼블릭이다.

## 함수스코프 
- funcion-level scope
- 함수 내에서 선언된 매개변수와 변수는 함수 외부에서는 유효하지 않다.
~~~
var a = 10;     // 전역변수
(function () {
  var b = 20;   // 지역변수
})();           // 선언과 동시에 실행 ()쓰기 
console.log(a); // 10
console.log(b); // "b" is not defined 선언된적없음 
~~~

~~~
//내지역에서 먼저찾고, 그다음 밖에서 x(선언문과 할당문)찾음
var x = 'global'; //전역에서 찾음
function foo() {
  var x = 'local'; 
  console.log(x); //지역에서 찾음 
}
foo();          // local
console.log(x); // global 전역에도 없으면 undefined나왔을것  
~~~

- 중첩 scope는 가장 인접한 지역을 우선하여 참조한다.
- 지역에서 쓰는함수는 내부함수에서 쓰고 버려. 밖에서 쓰려면 인자로 넘기기 
  .코드앞줄만 봐도 알수있게 function foo(인자값) 

  ### 암묵적전역
  - var 키워드없이 변수를 사용하면 암묵적으로 전역변수가 된다.주의하기 

~~~
  function foo() {
  x = 1;   // Throws a ReferenceError in "use strict" mode
  var y = 2;
}
~~~ 

- es6 들어와서 strict mode 안써도 
- 이런코드 에러잡기 힘들어(eslint쓰면 표시해줌)

- 함수가 선언된 시점에서의 유효범위를 갖는다. 

~~~
function foo (){
  // var i = 0;
  i = 0;
} 
~~~ 

-  {}안에있어도 var 빼먹으면 전역변수 

## 최소한의 전역변수 사용 

- 즉시 실행 함수(IIFE, Immediately-Invoked Function Expression)로 모두 지역변수로 쓰기 


<hr>

# this
- js에서 this는 함수의 현재 실행 문맥
- 자바스크립트의 함수는 호출될 때, 매개변수로 전달되는 인자값 이외에, arguments 객체와 this를 암묵적으로 전달 받는다.


## 1. 메소드 호출 패턴 
- 자신을 호출한 객체를 가리킴

~~~
var obj1 = {
  name: 'Lee',
  sayName: function() {
    console.log(this.name);
  }
}

var obj2 = {
  name: 'Kim'
}

obj2.sayName = obj1.sayName;
// obj1.sayName;는 funtion()가리키지만..

obj1.sayName(); //흰칸
obj2.sayName(); //녹색칸 
~~~ 
![](http://poiemaweb.com/img/Method_Invocation_Pattern.png)


(2)
~~~
function Person(name) {
  this.name = name;
}

Person.prototype.getName = function() {
  return this.name;
}

var me = new Person('Lee');
console.log(me.getName());

Person.prototype.name = 'Kim';
console.log(Person.prototype.getName());
~~~
// 두대가 this가 달라 


## 2. 함수호출패턴

- 함수호출에서 this는 전역객체

- 내부함수, 콜백함수도 this는 전역객체! 
  (내부함수내의 this가 전역가리킬경우 that쓰는방법)

- 함수호출 패턴에 따라 어떤 객체를 this에 바인딩할지 결정

> 전역객체(Global Object, 유일한 최상위객체)는 Browser-side에서는 window, Server-side(Node.js)에서는 global 객체
- 전역객체는 전역스코프를 갖고(전역변수를 프로퍼티로 갖음),전역에 선언한 함수는 전역객체의 프로퍼티로 접근할 수 있는  전역 변수의 메소드이다. 



(1)매서드로 호출될때 
~~~
var obj1 = {
  name: 'Lee',
  sayName: function() {
    console.log(this.name);
  }
}

var obj2 = {
  name: 'Kim'
}

obj2.sayName = obj1.sayName;

obj1.sayName();
obj2.sayName();
~~~
- 함수가 객체의 프로퍼티이면 메소드 호출 패턴으로 호출
- 메소드 내부의 this는 해당 메소드를 소유한 객체

- 기본적 this는 전역 
- 메소드의 내부함수 일때도 전역(js만)

객체=소속이있다 = 소속없는것 object 하나 
~~~
var value = 1;

var obj = {
  value: 100,
  foo: function() {
    setTimeout(function() {
      console.log("callback's this: ",  this);  // obj
      console.log("callback's this.value: ",  this.value); // 1 ?
    }, 100);
  }
};

obj.foo();
~~~
- 더글라스 크락포드 설계적 결함 
- this가 전역을 가르키지 않도록 하는 방법

~~~
var that= this; //(1)that을 만들어서 일단 킵 
~~~

### 3. 생성자 호출(실행)패턴
- 자바스크립트의 생성자 함수는 객체를 생성하는 것
- 기존함수에 new 연산자 붙여서 호출하면 
  this 바인딩이 메소드나 함수 호출 때와 다르게 동작

- new와 함께 생성자 함수를 호출하면, 생성자 함수 내부의 this는 생성자 함수에 의해 생성된 인스턴스를 가리킴
- 일반함수와 생성자 함수에 특별한 형식적 차이는 없기 때문에 대문자쓰기 

//함수실행
//프로퍼티 추가
//생성된 객체 리턴 
//생성자함수엔 returen안써. 프로퍼티 추가만해. 생성자 함수가 반환할 생성할 객체 



#### 4. apply 호출패턴에서 this

- apply()는 앞에 함수가 와야해. 그 함수를 *호출*하는것.
  그때 이 함수의 this값을 지정하는게 apply

~~~ 
//func이란 함수쓰고 .apply로 붙음  
func.apply(thisArg, [argsArray])

/* 함수 프로토타입
 첫번째 아규먼트 : 필수 하나이상 
 두번째 아규먼트 : 대괄호 있는건 옵션. 없어도됨
 apply()를
*/ 

var Person = function (name) {
  this.name = name;  //여기 this는 전역아니고 foo임
};

var foo = {}; // foo생성자 함수가 생성할 객체 

// apply메소드는 생성자함수 Person을 호출한다. 이때 this에 객체 foo를 바인딩한다.

Person.apply(foo, ['name']);

//배열은 인자의 리스트 . 매개변수=인자 1개 .여러개면 ,  로 씀 
console.log(foo); // { name: 'name' }
~~~ 

실무에서 많이쓰는 방식이다.  

~~~
function convertArgsToArray() { //convertArgsToArray이름의 함수생성 
  console.log(arguments);

  // arguments 객체를 배열로 변환하기 위해서 array 필요  
  // prototype의 속성인 slice에 접근. apply함수사용
  // 배열의 특정 부분에 대한 복사본을 생성
  var arr = Array.prototype.slice.apply(arguments); 
  // arguments.slice
  // var arr = [].slice.apply(arguments);

  console.log(arr);
  return arr;
}

convertArgsToArray(1, 2, 3);

~~~ 




> 배열은 순서대로

: 유사배열은 배열이 아님. dom의 쿼리결과, 아규먼트 객체


배열객체 array()생성자함수로 만듬, 배열리터럴 이나 new로 
그러면 array.prototype 에 여러 메소드 있는데 그중에 slice가 있어서 사용


> call() 과 apply()의 차이  

: call() 메소드의 경우, apply()와 기능은 같지만 apply()의 두번째 인자에서 배열 형태로 넘긴 것을 각각 하나의 인자로 넘긴다.
: apply()와 call() 메소드는 콜백 함수의 this를 위해서 사용되기도 한다.


