
# 자료형 (Data type)


## 기본자료형

> 1. Boolean :
- ture 와 false

> 2. null :
-  정의가 되어있지 않은 data (0도 아니고, ""도 아닌 값)

> 3. undefined :
- 선언은 되었지만 값을 할당하지 않은 변수가 가지는 값 

> 4. number : 
- 정수형과 실수형 (소수점)을 함께 표현한다.
- NaN (숫자가 아니다. Not a number): 문자를 숫자로 나눈결과  

> 5. String : 
- 다국어를 지원할수 있는 문자 포맷 .유니코드 
- 텍스트는 홀따옴표나 쌍따옴표로 묶는데 통일성 있어야함.
  (둘다쓸경우 ""밖에 '' , 혹은 '' 쓰고 ""로 묶기)
- 기본 자료는 변경 불가능하다 라는것의 의미 
~~~
  var m =1 // 메모리 상에 할당되있는 데이터. 선언과 할당 같이한것. 
  m = 10   //값을 바꾸는게 아니라 메모리 공간에 다시 10을 만들어서 찾는것. 
~~~
- 수정이 아니라 재할당 한것 
- 객체에 . 이 달려있고 {}함수가 있는것은 메서드라고 함

~~~
str = str.substring(0, 3);
console.log(str); // Str이 나올것.  
~~~
- str = 을 써줌으로써 재할당 된것
- 객체에 . 이 달린것 , 자바스크립트의 독특한 움직임. 기본자료형이 레퍼객체가 있어서 객체처럼 움직임. 

> 6. Symbol
- 데이터를 심볼이라는 함수로 만듬 
- es6 에서 추가된 타입 


## 객체형 (object type =참조형)
---

- 가장 많이 쓰는것을 객체형. 자바스크립트는 타 언어들과 객체가 좀 다름. 
- 객체안에는 데이터도 있고 함수도 있음
  메서드들이 객체 내부의 데이터를 조작하여 무언가 하는것. 
  비슷한 일을 하는것들끼리 묶음. 

- 프로퍼티의 값이 데이터이면 그냥 프로퍼티이고
  프로퍼티의 값이 함수이면 메서드(데이터와 관련된 동작)라고 함.

- html 파싱할때 class는 dom을 변경되면 돔내에는 wrapper class가 따로있어 배열로 들어가(클래스는 띄어쓰기하고 여러개 쓰니까)



# 변수 
- var 
- 값을 저장. 조회, 변경위해 이름을 지정. 
- 영문자 혹은 $로 시작함 
- 대소문자 구별 

> 참조한다 : 메모리에 저장한 데이터를 변수명을 가지고 꺼냄 

> = (동호 equal sign) : 같다가 아니고 오른쪽에서 왼족으로 할당 

- eslint는 아래처럼 쓰면 빨간줄. var 줄마다 쓰는 습관들이기  
~~~
var person = 'Lee',
    address = 'Seoul',
    price = 200;
~~~

- 값을 할당하지 안은 변수는 초기값 undefined가 들어가있음.
~~~
var x;
console.log(x); // undefined
console.log(y); // ReferenceError
~~~
- c언어는 선언시 똑같이 공간을 확보하나 쓰레기값이 쌓여있어서 그상태로 참조하면 이상한 값이 나올수 있음. 그래서 반드시 초기화 하라는 문법을 같이써주는데 자바스크립트는 알아서 undefined 라고 써져서 그 자체로 초기화가됨.

> ReferenceError : 선언하려고 했는데 참조하려고 했더니 참조할것이 없다 에러 


#### 변수의 중복 선언

- 여러사람이 개발할때 다른사람 소스코드 전부 읽지않고 내가 중복선언 할경우, 이전의 변수값이 변할위험이 있으므로 중복선언 허용되지만 쓰지말기. eslint에서 빨간줄.


#### 변수선언시 var 키워드 생략 

- 변수선언시 var키워드를 생략하면 전역변수가 됨. 
- 자바스크립트의 태생적 결함. 단순한 용도로 쓰려고 만든것이여서 설계적 결함이 있음.
- 프레임워크에서는 설정이 다되있음.


#### 동적타이핑

> 타이핑: 데이터의 타입을 정하는 행위

- 동적타이핑 (dynamic typing) : 자동으로 자료형이 결정 
외부적으로는 데이터타입을씀. 우리는 var n =1 을 썼지만 우리는 정수를 위한 변수다 라고 쓰지 안았지만 자바스크립트 엔진이 n 뒤에오는 숫자를 보고 판단함.

- 한계가 있음. 그래서 타입스크립트가 생김.

- 하나의 변수로 여러가지 데이터 타입을 재할당 하고있음. 돌려쓰기식 변수는 사용하지 말기 

~~~
var foo;
console.log(typeof foo);  // undefined
foo = null;
console.log(typeof foo);  // object
foo = {};  //껍데기만 있음 
console.log(typeof foo);  // object
~~~

#### 변수 호이스팅
- 선언도 하지 안은 변수를 선언이전에 사용 가능하다? 
- 다른 c-family언어와 차별되는 특징  
- var 선언문이나 function 선언문을 해당 Scope의 선두로 옮기는 것

~~~
console.log(foo); // ① undefined  레퍼런스 에러가 나와야할것같은데 참조가 되네.

var foo = 123;
console.log(foo); // ② 123
{
  var foo = 456;
}  
console.log(foo); // ③ 456

// 위처럼 함수{}코드블럭 안에서 변수를 선언하면 타언어에서는 123 과 456이 다른데 
자바스크립트는 중복선언이 됨. 콘솔값은 456이 나옴.
~~~


- 호이스팅은 var 선언문. function선언문, 모든 선언문이 Scope(스코프) 상위로 옮겨진것. 사실은 옮겨진것처럼 보이는것. 

+ 선언단계 : 변수등록 (스코프가 참조하는 대상)
+ 초기화단계 : 무조건 undefined 받고 시작
-- 위의 두단계를 var 키워드로 한번에 선언과 초기화 
+ 할당단계 : 실제값 입력


#### var키워드로 선언된 변수의 문제점 

- es5에서 변수를 선언할수 있는 방법을 var 키워드뿐.
- es6는 : let과 const 키워드를 도입
- 자바스크립트는 함수블럭만 지역임므로 전역변수 남발의 가능성이 있다. (전역변수는 어디서든 참조와 수정이 가능)   

> Function level scope : 

함수스코프, 선언된 변수는 함수내에서만 유효하다 

(함수내부에서 선언한 변수는 지역변수이며, 함수 외부에서 선언한 변수는 전역변수)

> Block level scope : 

코드블럭내 선언된 변수는 코드블럭 내에서만 유효하다  


- scope를 잘게 쪼개라

구문(스테이트먼트)를 묶은것= 함수 (){}이안에 있는것
function foo (){} 이 코드블럭은 하나의 독특한 방
지역(가로안에서는)에서는 밖을 참조할수 있음. 

- if(){} ....()이안은 지역이 아님 {}안에만 지역. 



## 기타  

- 노드환경 : server-side. vscode에서 출력되는거 노드의 환경 돔컨트롤 안되지만 네트워크 기능이 추가. 여러파일 하나씩 읽기   
- 자바스크립트 엔진 : client-side. 돔을 컨트롤 할수있음. 크롬브라우저 개발자도구 콘솔, 윈도우에선 프롬프트라고 깜빡거림 
- 위 둘이 중복되는 부분이 많아서 자바스크립트 엔지니어가 서버사이드로 이동하기 쉬워짐 


#### REPL
> "repl에서 돌려봐" : 터미널에서 노드환경 들어가서 코딩하는것   
~~~
$ node
~~~

- 기초문법 같아서 지금 vscode에 출력하면서 공부 가능


# 연산자 ( Operator)


## 1.산술연산자 
> ++ 증가
> -- 감소 

~~~
var x = 5;
var y = 2;
var z;

z = x + y;  // 7
z = x - y;  // 3
z = x * y;  // 10
z = x / y;  // 2.5
z = x % y;  // 1
z = x++;    // 5 선대입후증가
z = ++x;    // 7 선증가후대입    
z = x--;    // 7 선대입후감소 ..위의 값부터 이어짐  
z = --x;    // 5 선감소후대입    
~~~

문자열 연결 연산자 
원칙적으로 옳지않으니 주의할것 
~~~
var str1 = '5' + 5;      // '55'
var str2 = 5 + '5';      // '55'
var str3 = 'Hello' + 5;  // 'Hello5'
~~~

## 2. 대입연산자 
~~~
var x;
x = 10;   // 10

x += 5;   // 15   x = x+5 
x -= 5;   // 10   x = x-5
x *= 5;   // 50   x = x*5
x /= 5;   // 10   x = x/5 
x %= 5;   // 0    x = x%5 나눈뒤 나머지수 
~~~

## 3. 비교연산자

> == 는 한쪽이 숫자고 한쪽이 문자면 형 변환 
> === 형,타입 같아야 true 반환 . 정확  
> !=  이것도 형변환 되므로 !== 로 쓸것  

~~~
var x = 5

x == 5    // true
x == '5'  // true 형변환됨! 
x === '5' // false 이렇게씀 
~~~

> ? 삼항 연산자 (ternary operator)

~~~
// 조건 ? 조건이 ture일때 반환할 값 : 조건이 false일때 반환할 값
var condition = true;
var result = condition ? 'true' : 'false';
console.log(result); // 'true'
~~~

length 라는 프로퍼티가 있는데 .을 붙임으로써 모든 자료형은 레퍼클래스(wrapper class)가 있어서 기본형이 객체로 바뀌고 행위를 한후 다시 원상복귀
~~~
// id의 길이가 INPUT_ID_MIN_LEN보다 작으면 에러 메시지를 출력.
var id = 'lee';
var INPUT_ID_MIN_LEN = 5;
var errMsg = id.length < INPUT_ID_MIN_LEN ? '아이디는 5자리 이상으로 입력하세요' : '성공';
console.log(errMsg); // '아이디는 5자리 이상으로 입력하세요'
~~~



## 4. 논리연산자

|| : 둘중 하나를 리턴 
~~~
var o2 = false || true;     // true
var a2 = true && false;    // false

var n1 = !true;  // false
var n2 = !false; // true
var n3 = !'Cat'; // false
~~~


## 5. 단축평가 

- 논리연산자가 Boolean 값과 함께 사용되지 않을 경우, Boolean 값을 반환하지 않을 수 있다. 
- if문 쓸때 사용 
~~~
var foo = 'Cat' && 'Dog'  // 빈문자열이 아닌 문자열은 true로 인식. true면 뒤를 봐야함  returns 'Dog'

var foo = false && 'Cat' //false 면 뒤에 볼것도 없이 returns false

var foo = 'Cat' || 'Dog'  // foo는 t || t returns 'Cat'. 엔드는 뒤에 볼것도 없음 
~~~

## 6. 타입연산자 
- typeof  : 변수의 자료형을 문자열로 반환 
- instanceof : 다음시간 
~~~
typeof myCar                  // returns undefined (설계적 결함)
typeof null                   // returns object (설계적 결함)
~~~ 

## 7. !!
 
- 객체 \존재 확인후 결과를 반환할경우 !!는 불린형(true /flase)으로 변환 
~~~
console.log(!!1);         // true
console.log(!!0);         // false
console.log(!!'string');  // true
console.log(!!'');        // 빈것 부정적(null undefined) flase
~~~
//객체의 경우 빈객체라도 존재만 하면 문자열이 아니라 true 


> 코드블럭 : 
- 중괄호 시작하고 닫히는것. 객체 함수에 쓰임
- 구분의 집합을 한꺼번에 실행시키기 위한것 


# 제어문
---

## 1. 블록구문
## 2. 조건문

### if문
- if를 여러번 쓸수있어. else if 사용 
~~~
// if-else 문
if (hour < 18) {
  greeting = 'Good day';
} else {
  greeting = 'Good evening';
}
console.log(greeting);

// if-else if 문
if (hour < 10) {
  greeting = 'Good morning';
} else if (hour < 20) {
  greeting = 'Good day';
} else {
  greeting = 'Good evening';
}
console.log(greeting);

~~~

### switch문
- true false가아님 값을 봄
- 코드블럭이 오는게 아니고 그냥 case문을씀 
- 반드시 break를 써야 switch 구문에서 탈출함.
- red color 가 출력됨. 
- [c]+[a]+n : vscode에서 js파일에서 출력 
~~~
var color = 'red';

switch (color) {
  case 'yellow':
    console.log('yellow color');
    break;
  case 'red':
    console.log('red color');
    break;
  case 'blue':
    console.log('blue color');
    break;
  default:
    console.log('unknown color');
}
~~~ 

### for문
- 특정 조건이 거짓으로 판별될 때까지 반복한다. 
- 몇번반복할까?  i= 숫자와 조건문의 숫자 
- true 면 구문에서 증감문으로 반복  
- flase가 되야 빠져나옴 
~~~
for ([초기문]; [조건문]; [증감문]) {
  구문;
}
~~~

- 아래의 for문은 변수 i가 0으로 초기화된 상태에서 
i가 2보다 작아질 때까지 코드블럭을 반복 실행
- var i=0; 초기문은 한번만실행 for문을 돌리기위한 역활 
~~~
for (var i = 0; i < 2; i++) {
  console.log(i);
}
~~~

위 예제를 역으로 반복하는 for문의 예이다.
~~~
for (var i = 1; i >= 0; i--) {
  console.log(i);
}
~~~

- 무한루프
~~~
var i = 0;
for (;;) { // 무한루프
  if (i >= 3) {
    break;
  }
  console.log(i);
  i++;
}
~~~
- var i = 0을 위로뺌 
- i가 3보다 크면 탈출

> 디버깅

### while 문 
- 조건문이 참이면 코드 블럭을 계속해서 반복 실행
~~~
var n = 0;
var x = 0;

// n이 3보다 작을 때까지 계속 반복
while (n < 3) { // n: 0 1 2
  n++;          // n: 1 2 3 이 되면 n<3이니까 이제 안올라가고 빠짐 
  x += n;       // x: 1 3 6
  console.log(x);
}
~~~

~~~
var i = 0;
// 무한루프
while (true) {
  console.log(i);
  i++;
  // i가 10이면 exit! 
  // if (i === 10) break;
}
~~~
- 조건문이 언제나 참이면 무한루프
- 계속움직이는 게임배경
- 무한루프를 탈출하기 위해서는 break문을 사용 if

### do while문
- 코드블럭을 한번은 실행하고 조건을 봄

### continue 
- 어떤 조건에선 뒤에구문 생략해야함
- break문은 반복문 하나를 탈출한다.
- continue문은 이후 구문의 실행을 스킵하고 반복문의 조건문으로 이동한다.
~~~
for (var i = 0; i < 5; i++) { //5번 돌껀데 
  if (i % 2 == 0) continue;  //짝수이면 아무것도 안해. 쓰나안쓰나 같잖아?? 
  console.log(i);  //홀수만 출력 
}
~~~

### 평가
- 변수의 값을가지고 조건식을 달때 많이씀

~~~
if (1) { //언제나참 쓸필요없지 
  console.log('1');
}

if ('str') {  // 이거많이써. 이문자열 true가됨. 변수가 비어있는 문자열이 아닌 실제 문자열이면 무언가 해야할때가 있지. 인자체크.. 
  console.log('2');
}

if (true) {
  console.log('3');
}

if (null) { // null은 flase 실행안되 
  console.log('4');
}

var x = ''; // false 빈문자열 

if (x) {   // false  
  console.log('5');
}

if (!x) {  // true
  console.log('6');
}
~~~

#### 암묵적 강제형변환 (type coercion)
- 연산자가 돌아갈수있도록 엔진이 최대한 변환
- 실무에선 명확하게 써야함 
~~~
console.log('1' > 0);            // true / 부등호때문에 강제 형변환됨
console.log(1 + '2');            // '12' /
console.log(2 - '1');            // 1 /  '1'은 숫자로 변환

console.log('10' == 10);         // true
console.log('10' === 10);        // false
console.log(undefined == null);  // true  /둘다부정적이라
console.log(undefined === null); // fal   /타입까지 보니까 
~~~

> Type Conversion Table : 패턴이해해서 외우기 
> Data type conversion 

(1) sting -> number 변환하는 방법 
~~~
val *= 1;  //벨류는 벨류 곱하기 1 . 결론적으로 숫자가됨 .편리한방법 외우기 
// val = Number(val);  위와같음 
// val = parseInt(val);
~~~

(2) number -> sting  변환하는 방법 
~~~
val += '';
// val = String(val);
console.log(typeof val + ': ' + val); // string: 123
~~~


#### Checking equality
- 이해한대로안되.. 예측블가능
- 두 값을 비교할 때에 동등연산자(==, !=)보다 일치연산자(===, !==)를 사용해야
~~~
// logs false !!!
console.log(null == false);
console.log(undefined == false);
console.log(null == 0);
console.log(undefined == 0);
console.log(undefined === null);
console.log(NaN == null);
console.log(NaN == NaN);
~~~

#### Checking existence
- 객체나 배열(배열도 객체이다)이 값을 가지고 있으면 truthy value로 취급된다.
~~~
if (document.getElementById('header')) {
  // 요소가 존재함 true : 필요한 작업을 수행
} else {
  // 요소가 존재하지 않음 false : 필요한 작업을 수행
}
~~~

- 아래는 객체를 true랑 비교한것. 이렇게 하면 안되 
~~~
if (document.getElementById('header') == true) // false
~~~ 

~~~
var b = new Boolean(false); //래퍼클래스 
if (b) // true   폴스값을 갖고있는객체라고 객체가있음- 이라고 판정되서 true가 나옴 
~~~

<br>

# 객체(Object)란?

- 자바스크립트는 객체기반의 스크립트 언어
- 기본자료형을 제외한 나머지 값들(함수, 배열, 정규표현식 등)
- 데이터와 그 데이터에 관련되는 동작을 모두 포함하여 말함. 
- 이름(키)과 값으로 구성된 데이터를 의미하는 프로퍼티와 동작을 나타내는 메서드를 포함 
- 객체는 데이터를 한 곳에 모으고 구조화하는데 유용
- 객체 하나는 다른 객체를 포함할수있음  

### 프로퍼티
- 값을 꺼내오기위한 하나의 키
- 이름(name)과 값(value)의 쌍인 프로퍼티들을 포함하는컨테이너
프로퍼티 이름 : 빈 문자열을 포함.(문법적으로 허용되나안씀) 문자열과 숫자
프로퍼티 값 : undefined을 제외한 모든 값

### 메서드 (Method)

## 객체생성방법
> (1) 중괄호({})를 사용하여 객체를 생성
~~~
var emptyObject = {}; // 중괄호 이건 코드블럭이 아니고 객체. 프로퍼티가 없다. 중괄호를 열고닫음으로써 객체를 생성할수있다. 클래스 필요없네
console.log(typeof emptyObject); // object 라고 딱 나와 . 위에껀 빈객체
~~~
- 객체리터럴 
~~~
var person = {
  name: 'Lee',  //name이 프로퍼티명 : 'Lee'는 프로퍼티값 
  gender: 'male',
  sayHello: function () { //값으로 달린 이 function이실행 
    console.log('Hi! My name is ' + this.name);
  }
};
//콘솔로그에 뭐라고써야 나온다고? 
// 변수의 우항에 객체리터럴 방식 으로 할당 
~~~

- , 컴마로 구분 
- 이렇게써야 사람이라는 객체가 만들어짐.
- json은 객체와 거의 유사 
- person은 2개의 데이터와 한개의 메서드를 갖고있음
- this 는 person이다 
- 객체내에서 메서드가 다른 프로터리를 지칭할때는 this를쓴다(중요)

- person이라는 변수에 객체리터럴 이 할당됨.


> (2) object 생성자 함수
- Object() 생성자 함수를 new연산자와 함께 사용하면 빈객체 만들어짐
- 문법을 자바 흉내낸것
- 우리가 이렇게 쓸일이 없고, 우리는 (1)처럼 객체를 생성하는 코드를쓰면 자바스크립트엔진이 내부적으로 Object() 생성자 함수를 사용하여 객체를 생성한다. 
~~~
// 빈 객체의 생성
var person = new Object();  //빈객체 만듬 
// 프로퍼티 추가
person.name = 'Lee';  // 프로퍼티 생긴뒤에 여기에 값 넣음
person.gender = 'male';
person.sayHello = function () {  // 프로퍼티 생기고 함수넣고 
  console.log('Hi! My name is ' + this.name);
};
~~~

> (3)생성자함수
- this를 써서 프로퍼티를 하나하나 만들어줌
- 유사객체 대량 생산해야할때 
- 생성자 함수 이름은 대문자로 시작하여, 생성자함수란것을 알린다  
~~~
// 생성자 함수 만들고 
function Person(name, gender) {
  this.name = name;
  this.gender = gender;
  this.sayHello = function(){
    console.log('Hi! My name is ' + this.name);
  };
}

// 인스턴스(실제객체)의 생성하기 new  
var person1 = new Person('Lee', 'male');
var person2 = new Person('Kim', 'female');

console.log('person1: ', typeof person1);
console.log('person2: ', typeof person2);
console.log('person1: ', person1);
console.log('person2: ', person2);
~~~ 

- 한두개일땐 간단하게 객체생성방식. 여러개일땐 생성자함수로 쓰기 


## 객체 프로퍼티 접근

### 프로퍼티 이름
~~~
var person = {
  'first-name': 'Ung-mo', //(-)연산해버리니까 ''따옴표 같이쓰고 ..쓰지말기 
  'last-name': 'Lee',  //_ 쓰면 따옴표 안써도되 
  gender: 'male',
  function: 1 // OK. 하지만 예약어는 사용하지 말아야 한다.
};

console.log(person.function);
~~~


> 이름쓰는법 
First_name : 씀.  
FirstName : 단어다를때 대문자, 가장많이씀
First-name : 쓰지안음. 예약어(오류는안나)도 변수명 프로퍼티명으로 쓰지마세요.
변수는 : 명사쓰기 
메서드는 : 동사 + 목적어

### 프로퍼티 값읽기

- 마침표(.) 표기법  : 이거쓰면 객체화 
- 대괄호[] 표기법  
~~~
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male',
};

console.log(person.gender);    // 'male'
console.log(person[gender]);   // Reference에러 
console.log(person['gender']); // 'male'

console.log(person.first-name);    // NaN: undefined-name
console.log(person[first-name]);   // ReferenceError: first is not define
console.log(person['first-name']); // 'Ung-mo' 대괄호안에는 반드시 ''씀 
~~~

- 객체에 존재하지 않는 프로퍼티를 참조하면 undefined를 반환
~~~
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male',
};
console.log(person.age); // undefined 레퍼런스에러가 아님 
~~~

### 프로퍼티 값 갱신
- 객체가 소유하고 있는 프로퍼티에 새로운 값을 할당하면 프로퍼티 값은 갱신된다.
### 동적생성
- 객체가 소유하고 있지 않은 프로퍼티에 값을 할당하면 하면 해당 프로퍼티를 객체에 추가하고 값을 할당한다.
### 프로퍼티 삭제
- delete 연산자를 사용하면 객체의 프로퍼티를 삭제할 수 있다.
~~~
var person = {
  'first-name': 'Ung-mo',
  'last-name': 'Lee',
  gender: 'male',
};

delete person.gender;
console.log(person.gender); // undefined

delete person;
console.log(person); // Object {first-name: 'Ung-mo', last-name: 'Lee'}
~~~

###  for-in 문
- 객체에 포함된 모든 프로퍼티에 대해 루프를 수행할 수 있다.
- es6에서 나온 for-of를 쓰라고함

## pass-by-reference

- 기본자료형은 새로운 값입력하면 중복할당
- 객체는 참조(주소)값을 준다 = 단일객체를 쓴다: 어디서 바뀌든 하나임으로 
- 객체는 참조형이므로  다른 변수에 대입했을때도 두 변수는 똑같은 객체를 가르킨다(둘다영향), 객체를 나눠담은것은 용도가 달랐을텐데  다른한쪽에서 변수를 예상치 못하게 바꾸면 문제가 생김

~~~
var foo = obj;
// foo 값바꾸면 obj도 바뀜
~~~ 
// 객체값이 넘어가는게 아니라 



## pass-by-value
기본자료형의 값은 값(value)으로 전달. 복사되어 전달. 한번 정해지면 변경불가


> 객체의 분류 

![Alt](http://poiemaweb.com/img/object.png)
+ host object : 우리가 만든 것 
+ built-in object : 자바스크립트가 만들어 놓은것 
 - standard Build-in : string , number, array 객체, 프로퍼티, 메서드 
 - native object  : 
  + bom : browser object model 이건안배워.  
  + dom : documnet object model css가 파싱된 결과 씨쏨.html정보갖는객체 


> 데이터타입이 왜 필요한가? 
: 메모리를 효과적으로 쓰기위해서 

- 객체는 프로퍼티를 자유롭게 추가시킬 수 있어서 메모리를 몇바이트로 잡아줘야할지모름. 클확률이 높아서 복사해서 쓰기시작하면 위험. 그래서 pass-by-value를 쓰는데 문제 일으킬수 있다.


### 객체의 변경불가성
