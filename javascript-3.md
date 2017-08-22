# 함수

- 함수도 객체지만 호출 가능
> 호출 : 함수를 실행시키는 행위 (실행시킬때 함수에 필요한 값을 전달)
- 구문(statement)의 집합
- 코드의 재사용
- 함수도 객체이므로 프로퍼티가 있음(자바스크립트 엔진이 알아서만듬) 다른 값들처럼 사용 (기본값 빼고는 다 객체)

## 함수정의 
- 함수만드는 3가지 방법

### (1) 함수선언식 
: 함수명 생략할수없다 
: function 키워드와 이하의 내용(함수명오고 {})으로 구성
> 매개변수= 파라미터
1. 함수명
: 자신을 호출(재귀적 recursive 호출), 
2. 매개변수 
: 여러개일수. (,)로구분 
3. 함수몸체 
: 중괄호({ })로 구문들을 감싸고 return 문으로 결과값을 호출한 사람에게 return반환한다 
~~~
function square(number) { // number가매개변수 
  return number * number;
}
// return만 쓰면 undifined
// 보통 하나의 값으로 수렴되는식이 들어와
// return 문으로 결과값을 반환 =반환값  
~~~
- 앵귤러가 타입스크립트 정식채용하면서 타입스크립트 배워야 앵귤러 쓸수있어서 리액트가 뜸. 타입스크립트 많이쓰고있는데. 안쓰면 타입체크(넴버?문자?) 알려고 매개변수에 체크 넣어야함.
- 밖에서부터 값이맞는지 체크하고 {}안을 코딩
- typeof로 형을 보고 true/false를 판단  
- 연습에선 false라 빠지려면 return만 쓰면 되는데
실제론 예외처를 해야함
- 이래서 타입스크립트를 사용 

### (2) 함수표현식 :
: 함수명 써도되고 안써도 되고 
~~~
// 기명 함수표현식 : 재귀함수나 디버거를 위해씀
var foo = function multiply(a, b) {
  return a * b; // 호출하고 빠져나감. return안쓰면 undefined나옴 
};
// 익명 함수표현식 : 생략이 일반적 
var bar = function(a, b) {
  return a * b;
};
~~~

- 함수는 일급객체이기 때문에 변수에 할당가능 
> 일급객체 특징:
무명의 리터럴로 표현이 가능. 함수에이름없음.
변수나 자료 구조(객체, 배열…)에 저장가능.
함수의 파라미터로 전달가능.
반환값(return value)으로 사용가능 .

- funtion()여기 함수 넣으면 복잡하기 때문에 콜백함수를 사용 

~~~
var foo = function(a, b) { //a,b는 매개변수명= 인자=파라미터 
  return a * b;
};

var bar = foo;
console.log(foo(10, 10)); // 100 
// (10,10) 매게변수에 할당할값 = 인수 =아규먼트
// a에 10이 할당되고 b에 10이 할당됨

console.log(bar(10, 10)); // 100 함수실행값 
~~~
- 함수표현식은 변수명으로 호출
- 함수선언식은 함수명으로 호출 
: 함수선언식도 변수명과 함수명이 같기때문에 에러가 나지 안는것. 결국 표현식과 같음 사용하기 쉬우라고(문법적 설탕) 



### (3) Function() 생성자 함수 :

- 오브젝트 생성자함수는 빈객체를 생성했는데 
- 얘는 내용이 있는 객체생성 가능.

~~~
var square = new Function('number', 'return number * number');
console.log(square(10)); // 100
~~~

- 함수선언식은 기명함수표현식과 같은데 두 함수 리터럴 방식으로 함수를 정의하는데 이것은 결국 내장 함수 Function() 생성자 함수로 함수를 생성하는 것을 단순화 시킨 것
- 이것도 우리가 쓰는게 아니라 자바스크립트 엔진이 사용 


- 변수호이스팅과 함수호이스팅 뭐가다른가?
함수선언식으로 정의된 함수는 js엔진이 스크립트가 로딩되는 시점에 바로 초기화하고 이를 VO(variable object)에 저장


- 함수 선언의 위치와는 상관없이 소스 내 어느 곳에서든지 호출이 가능하다.
문제점은 없는가?
~~~
var res = square(5); // TypeError: square is not a function 변수호이스팅이됨 

var square = function(number) {
  return number * number;
}
~~~
- 함수호이스팅이 아니라 변수 호이스팅이됨. 
- 스퀘어를 가지고 함수를 실행하려고 보니 값이 undefined. 스퀘어 함수가 아니라고 나와
- 함수선언식처럼 실행되는 거보다 위처럼 에러가 보이는게 좋기때문에 함수표현식을 추천하는것
- 그리고 반드시 호출전에 선언할것

~~~
// 2. 함수의 파라미터(parameter, 인자)로 전달 할 수 있다.
function calc(func, num){
  return func(num);
}
~~~ 

## 매개변수 
- 함수 내에서 변수와 동일하게 메모리 공간을 확보하며 전달되어진 인수는 매개변수에 할당되며, 인수가 전달되지 않으면 매개변수는 undefined로 초기화

> Call-by-value
: 값에 의한 호출로 동작
: 기본자료형 인수를 함수에 매개변수로 전달시 매개변수에 값을 복사하여 함수로 전달하는 방식
: 함수 내에서 매개변수를 통해 값이 변경되어도 전달이 완료된 기본자료형 값은 변경되지 않음 

> Call-by-reference
: 참조에 의한 호출로 동작
: 함수 내에서 매개변수의 참조값이 이용하여 객체의 값을 변경했을 때 전달되어진 참조형의 인수값도 같이 변경

## 반환값

- 함수는 반환을 생략할수있다(return키워드를 안쓸수도, undefined가 반환)
- 함수의 실행을 중단= 빠진다 
- return 키워뒤의 구문은 실행안됨


## 함수 객체의 프로퍼티

### arguments(인수) 프로퍼티
- 함수호출시 전달된 arguments들의 정보를 담고 있는 순회가능한유사 배열 객체읻.
- arguments 객체를 값으로 가지며 함수 내부에서 지역변수처럼 사용

> 유사배열객체 : length 라는 프로터가 있어서 자신의 개수를 암. 반복문을 돌릴수있어. 

~~~
function sum() {
  // arguments 객체를 배열로 변환
  var array = Array.prototype.slice.call(arguments); //아규먼트가 어레이의 배열로 들어가고 
  return array.reduce(function (pre, cur) {  //배열의 reduce함수사용 
  // 매게변수가 함수네..그러면 reduce라는 행위를 하면서 이 함수를 씀 
    return pre + cur;
  });
}

console.log(sum(1, 2, 3, 4, 5)); // 15
~~~

- 배열처럼 움직이지만 배열메서드를 쓰면 에러 
- slice는 함수 메서드. 배열을위한 매서드 
- arguments는 배열이 아님. 그냥쓰면 에러나서 .call 함수를 씀 

### caller 프로퍼티 
: 호출자
: 인자로 함수를 받고 함수를 실행 
~~~
function foo(func) {  //인자 
  var res = func();  //함수를실행. 실행한결과가 res에 담길것 
  return res;
}

function bar() {
  if (bar.caller == null) { //콜러가 없네 전역에서 바로 호출한것  
    return 'The function was called from the top!';
  } else {
    return 'This function\'s caller :\n' + bar.caller;
  }
}

console.log(foo(bar)); //bar.caller
console.log(bar());
~~~

### length 프로퍼티 
: 함수 정의 시 작성된 매개변수 갯수
: arguments.length의 값과 다름 (함수 호출시 인자의 갯수 )



### __proto__ 프로퍼티
- 모든 객체는 자신의 프로토타입을 가리키는 [[Prototype]]이라는 숨겨진 프로퍼티를 가진다. 크롬, 파이어폭스 등에서는 확인가능 

### prototype 프로토타입 프로퍼티
- 함수객체는 프로토타입 프로퍼티를 갖음

> prototype 프로퍼티 : 
- 모든객체가 갖고있는 프로퍼티
- 자신의 부모역할을 하는 프로토타입 객체를 가리키며 함수 객체의 경우 Function.prototype를 가리킴.

> [[prototype]] 프로퍼티 : 
- 생성자 함수가 생성한 객체의 부모역활을 할 객체를 가리킨다. 


<기타>
- 모든 객체는 부모가있다

- 객체를 생성하는 함수 =생성자함수 (내부에서 객체를 만듬 this name은뭐. this gender는 뭐)
- 함수 객체이기 때문에 펑션프로토타입 ...
- 이 프로토타입은 브라우저 확인가능한데 그걸 따라가면 부모를 가리키고있어.

- 일반함수와 생성자함수 구별할줄알아야 : 연산만 하고 객체를 생성하지 안음 

- 부모에 설정을 person.protorype 에 하면 밑에 여러개를 써도 같으니까

### 프로토타입의 프로퍼티 
- 생성자 함수가 객체를 생성했을때 그 부모를 따라갈수 있는것.
- 객체들에게 각각의 똑같은 메서드를 만들면 불합리 하므로 부모쪽으로 옮기면 편할것
- 메서드를 안에서 생성하지 않고  person.prototype 쓰고 메서드를 작성하면 가능

~~~

function square(number) {
  return number * number;
}

// console.dir(square);
console.dir(square.__proto__);  //function 
console.dir(square.prototype);  // 

~~~

- square.pototype  쩜찍힌애 프로토타입 객체


## 함수의 종류 

### 즉시호출함수표현식 (IIFE) 
: 선언과 동시에 호출
(읿반함수는 분리되어있음) 영어이름 기억하기  

~~~
// 기명 즉시실행함수(named immediately-invoked function expression)
(function myFunction() {
  var a = 3;
  var b = 5;
  return a * b;
}());
~~~
- ()가로로묶어 변수명충돌문제 방지 
- 초기 자바스크립트 전역에 쓰라고 만든언어. 그래서 es쓰는것. 이걸 안썼을때 iife를 썼음 



### 내부함수 
- 클로저와 관계
- 
### 콜백함수
- callback : 나중에 필요할때 실행된다
- 비동기식 처리모델에 사용(처리가 종료되면 호출될함수=콜백함수를 미리 매개변수에 전달하고 처리가 종료하면 콜백함수를 호출하는것 )
- 함수를 명시적으로 호출하는 방식이 아니라 특정 이벤트가 발생했을 때
- 많이쓰는 이벤트핸들러 처리 예  
~~~
 var button = document.getElementById('myButton');
    button.addEventListener('click', function() {
      console.log('button clicked!');
    });
~~~
- document 돔객체의 가장 대가리 (.)이으니 객체겠찌
- get ElementByID : 돔api를 부르면 
- button에 담음
- addEventListener : 이벤트를 등록하는 함수
- click 이라는 이벤트
- {}안에 있는 함수를 실행하라 
 

###

~~~
setTimeout(function () {
  console.log('1초 후 출력된다.');
}, 1000);
~~~ 
window. 생략된것
setTimeout , alert 전역함수

